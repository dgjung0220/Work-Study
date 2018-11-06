#### tfrecord reader

```
%matplotlib inline
import tensorflow as tf
from PIL import Image
import io
import matplotlib.pyplot as plt
```

```
tfrecord_filename = '/work/nas2/images/ObjectDetection/tfrecord/tfrecord_0913/OD_train.tfrecord-00004-of-00512'
```

```
def readRecord(filename_queue):
    reader = tf.TFRecordReader()
    _, serialized_example = reader.read(filename_queue)
    
    keys_to_features = {
        'image/height': tf.FixedLenFeature((), tf.int64, 1),
        'image/width': tf.FixedLenFeature((), tf.int64, 1),
        'image/filename': tf.FixedLenFeature((), tf.string, default_value=''),
        'image/key/sha256': tf.FixedLenFeature((), tf.string, default_value=''),
        'image/source_id': tf.FixedLenFeature((), tf.string, default_value=''),
        'image/encoded': tf.FixedLenFeature((), tf.string, default_value=''),
        'image/format': tf.FixedLenFeature((), tf.string, default_value='jpeg'),

        # Object boxes and classes.
        'image/object/bbox/xmin': tf.VarLenFeature(tf.float32),
        'image/object/bbox/xmax': tf.VarLenFeature(tf.float32),
        'image/object/bbox/ymin': tf.VarLenFeature(tf.float32),
        'image/object/bbox/ymax': tf.VarLenFeature(tf.float32),
        'image/object/class/label': tf.VarLenFeature(tf.int64),
        'image/object/class/text': tf.VarLenFeature(tf.string)
    }

    features = tf.parse_single_example(serialized_example, features=keys_to_features)

    height = tf.cast(features['image/height'], tf.int64)
    width = tf.cast(features['image/width'], tf.int64)
    filename = tf.cast(features['image/filename'], tf.string)
    source_id = tf.cast(features['image/source_id'], tf.string)
    encoded = tf.cast(features['image/encoded'], tf.string)
    image_format = tf.cast(features['image/format'], tf.string)
    xmin = tf.cast(features['image/object/bbox/xmin'], tf.float32)
    ymin = tf.cast(features['image/object/bbox/ymin'], tf.float32)
    xmax = tf.cast(features['image/object/bbox/xmax'], tf.float32)
    ymax = tf.cast(features['image/object/bbox/ymax'], tf.float32)
    label = tf.cast(features['image/object/class/label'], tf.float32)
    text = tf.cast(features['image/object/class/text'], tf.string)

    return height, width, filename, source_id, encoded, image_format, xmin, ymin, xmax, ymax, label, text
```

```
filename_queue = tf.train.string_input_producer([tfrecord_filename])
height, width, filename, source_id, encoded, image_format, xmin, ymin, xmax, ymax, label,text = readRecord(filename_queue)

init_op = tf.global_variables_initializer()

with tf.Session() as sess:
    sess.run(init_op)

    coord = tf.train.Coordinator()
    threads = tf.train.start_queue_runners(coord=coord)

    vheight, vwidth, vfilename, vsource_id, vencoded, vimage_format, vxmin, vymin, vxmax, vymax, vlabel,text = sess.run([height, width, filename, source_id, encoded, image_format, xmin, ymin, xmax, ymax, label, text])
    
    print(vwidth, vheight)
    print(vfilename)
    print(vlabel)
    print(text)
    image = Image.open(io.BytesIO(vencoded))
    plt.imshow(image)

    coord.request_stop()
    coord.join(threads)
```