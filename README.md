# ML_Sec_Lab4

```bash
├── data
    ├── cl
        ├── valid.h5 // this is clean validation data used to design the defense
        └── test.h5  // this is clean test data used to evaluate the BadNet
    └── bd
        ├── bd_valid.h5 // this is sunglasses poisoned validation data
        └── bd_test.h5  // this is sunglasses poisoned test data
├── models
    ├── bd_net.h5
    ├── bd_weights.h5
    ├── model_X=2.h5 //increasing order of activations
    ├── model_X=4.h5 //increasing order of activations
    ├── model_X=10.h5 //increasing order of activations
    ├── model_X_2.h5 //decreasing order of activations
    ├── model_X_4.h5 //decreasing order of activations
    └── model_X_10.h5 //decreasing order of activations
├── architecture.py
├── eval.py // this is the evaluation script
├── Evaluation using script given.ipynb
├── ML_Sec_Lab4_Channels pruned in decreasing order.ipynb //notebook with prescribed task
└── ML_Sec_Lab4_Channels pruned in increasing order.ipynb //notebook with second experiment as first gave suspicious results
```

## I. Dependencies

   1. Python 3.6.9
   2. Keras 2.3.1
   3. Numpy 1.16.3
   4. Matplotlib 2.2.2
   5. H5py 2.9.0
   6. TensorFlow 

## II. Data

   1. Download the validation and test datasets from [here](https://drive.google.com/drive/folders/1Rs68uH8Xqa4j6UxG53wzD0uyI8347dSq?usp=sharing) and store them under `data/` directory.
   2. The dataset contains images from YouTube Aligned Face Dataset. We retrieve 1283 individuals and split into validation and test datasets.
   3. bd_valid.h5 and bd_test.h5 contains validation and test images with sunglasses trigger respectively, that activates the backdoor for bd_net.h5.

## III. Generate Good Models

   1. Run `ML_Sec_Lab4_Channels pruned in increasing order.ipynb` or `ML_Sec_Lab4_Channels pruned in decreasing order.ipynb` by opening it in your favourite python notebook viewer/editor.
   2. This will generate / overwrite the repaired models.
   3. Then run `Evaluation using script given.ipynb` to evaluate using given script.
   4. Either of the three notebooks will evaluate and print the Accuracy and Attack Success Rate of these models using the given evaluation logic but if you want you can test the same using the `eval.py` script as outlined below.

      ### Note:
      ### I had to use Google Colab Pro when running `ML_Sec_Lab4_Channels pruned in increasing order.ipynb` because of memory constraints.
      

## IV. Evaluating the Backdoored Model

   1. The DNN architecture used to train the face recognition model is the state-of-the-art DeepID network.
   2. To evaluate the backdoored model, execute `eval.py` by running:
      `python3 eval.py <clean validation data directory> <poisoned validation data directory> <model directory>`.

      E.g., `python3 eval.py data/cl/valid.h5 data/bd/bd_valid.h5 models/bd_net.h5`. This will output:
      Clean Classification accuracy: 98.64 %
      Attack Success Rate: 100 %

## V. Important Notes

Please use only clean validation data (valid.h5) to design the pruning defense. And use test data (test.h5 and bd_test.h5) to evaluate the models.

When performing the experiment, pruning channels in decreasing order of average activations, the results were suspicious, so I ran another expirement, this time by pruning channels in increasing order of average activations.
