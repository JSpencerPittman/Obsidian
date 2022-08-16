# Photo OCR
OCR = Optical Character Recognition
## Pipeline
1. Text Detection
2. Character Segmentation
3. Character Classification
A pipeline has multiple sequential machine learning components
Offers a way to divide up the workload

Distortions should be representative of the test set
It's usually unproductive to add random/meaningless noise to your data

Make sure you have a low bias classsifiar before expending the effor. Learning Curves can be used to find this out.

How much work would it be to get 10x as much data as we currently have?
One way may be artificial data synthesis
Another is to collect/label it yourself
Crowd Source

## Ceiling Analysis
See overall accuracy in a system if each component on a pipeline was improved
