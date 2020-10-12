# Estimate Your Model

[![Language grade: Python](https://img.shields.io/lgtm/grade/python/g/peteryuX/retinaface-tf2.svg?logo=lgtm&logoWidth=18)](https://lgtm.com/projects/g/peteryuX/retinaface-tf2/context:python)
![License](https://img.shields.io/github/license/peteryuX/retinaface-tf2)


:fire: I think estimating your model is a very important step to elevate your project preformance. :fire:

>For example, if our project is a object detection task.
>
>We can estimate our model by mAP, recall and precision.
>
>And the outputs of object detection model are scores, location and classification.
>
>We need to use scores to judge positive or negative objects.
>
>Use small score to be the threshold can rise recall.
>
>But, the precision maybe go down because the precision is related to IOU.
>
>So, you can use grid search to decide which score is the best threshold.
>
>And I used to set IOU be 0.5.
>
>:pizza:Use mAP to estimate your object detection model and enjoy it!
>
>****

****

## Contents
:bookmark_tabs:

1. [Recall]()
2. [Precision]()
3. [mAP]()
4. [AUC]()
5. [ROC]()

***

### Recall

You can use recall to estimate your binary model like image classification and you can also use it to estimate your object detection task.

In binary model:

```mathematica
recall = TP / (TP +FN)
```

In object detection:

```mathematica
recall = TP / gtp
```

gtp is ground truth positive.

### Precision

```mathematica
precision = TP / (TP + FP)
```

### mAP

mAP - mean accuracy precision.

mAP is a very important metric in object detection.

```python
1.Get positive objects that score > 0.3
2.sort the positive objects in a descending order
3.caculate ap for every class
4.TP = [0] * num_positive
5.FP = [0] * num_positive
6.for idx, obj in positives:
    if max_iou > iou_threshold:
        TP[idx] = 1
    elif max_iou < iou_threshold:
        FP[idx] = 0
7.caculate AP for each class
8.Firstly, you need to make the precision monotonically decreasing
######################################################################
# matlab indexes start in 1 but python in 0, so I have to do:
#     range(start=(len(mpre) - 2), end=0, step=-1)
# also the python function range excludes the end, resulting in:
#     range(start=(len(mpre) - 2), end=-1, step=-1)
for i in range(len(mpre)-2, -1, -1):
	mpre[i] = max(mpre[i], mpre[i+1])
######################################################################
9.Secondly, get the area under precision curve
```

### AUC（Area Under ROC Curve）

AUC is the area under ROC curve, the higher the ROC is and the better the model is.

### ROC

The x is False Positive Rate, the y is True Positive Rate.

<img src="./img/roc.jpg" align="center" width="550">

### ToDO

* [ ] lamr(log average miss rate)



