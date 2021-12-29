# QSORT

QSORT(Quick + Simple Online and Realtime Tracking) is a simple online and realtime tracking algorithm for 2D multiple object tracking in video sequences. It is much faster than [SORT(Simple Online and Realtime Tracking)](https://arxiv.org/abs/1602.00763). But its performance is a little worse than SORT.

This method and project are heavily based on [abewley/sort](https://github.com/abewley/sort).

**Note:** A significant proportion of QSORT's accuracy is attributed to the detections.
For your convenience, this repo also contains *Faster* RCNN detections for the MOT benchmark sequences in the [benchmark format](https://motchallenge.net/instructions/). To run the detector yourself please see the original [*Faster* RCNN project](https://github.com/ShaoqingRen/faster_rcnn) or the python reimplementation of [py-faster-rcnn](https://github.com/rbgirshick/py-faster-rcnn) by Ross Girshick.

## What is different from SORT?

QSORT is SORT skipping the Kalman Filter. That's it.

## Dependencies:
To install required dependencies run:
```
pip install -r requirements.txt
```

### Demo:

To run the tracker with the provided detections:

```
cd path/to/qsort
python qsort.py
```

To display the results you need to:

1. Download the [2D MOT 2015 benchmark dataset](https://motchallenge.net/data/MOT15.zip) and unzip this file.
0. Create a symbolic link to the dataset
```
ln -s /path/to/MOT15 MOT15
```
0. Run the demo with the ```--display``` flag
```
python qsort.py --display
```

### Main Results

Using the [MOT challenge devkit](https://github.com/JonathonLuiten/TrackEval) the method produces the following results (as described in the paper).

Method | MOTA | IDs | FPS
--------------- |:----:|:----:|:----:|
[SORT](https://github.com/abewley/sort#main-results) | 34.0| 274 | 742 |
QSORT| 31.7| 344| 2194 |
- Sequence: TUD-Campus, ETH-Sunnyday, ETH-Pedcross2, ADL-Rundle-8, Venice-2, and KITTI-17
- MOTA, FPS: Higher is better.
- IDs: Lower is better.

FPS is measured on a Intel I5 10400 CPU.

### Using QSORT in your own project

Below is the gist of how to instantiate and update SORT. See the ['__main__'](https://github.com/developer0hye/qsort/blob/main/qsort.py#L251-L253) section of [qsort.py](https://github.com/developer0hye/qsort/blob/main/qsort.py) for a complete example.

```python
from qsort import *

#create instance of QSORT
mot_tracker = QSORT() 

# get detections
...

# update QSORT
track_bbs_ids = mot_tracker.update(detections)

# track_bbs_ids is a np array where each row contains a valid bounding box and track_id (last column)
...
```
 
