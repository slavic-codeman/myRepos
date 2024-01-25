## 1. Installation

The code has been tested on Windows PowerShell using python 3.10.

And you need to install following python libraries to run the code.

1. **Install PyTorch with CUDA 12.1**

   You can use command from [pytorch.org](https://pytorch.org/) to install them.

   ```
   pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu121
   ```

2. **Install Other Libraries**
   
   Check requirements.txt for other packages required.
   You can use following command to download all the packages.
   ```
   pip install -r requirements.txt
   ``` 
      

## 2. GatyStyle and LapStyle

1. **Run with Default Settings**

   To run with default settings, you can simply use command 

   ```
   python GatyStyle.py
   ```

   or

   ```
   python LapStyle.py
   ```

   in Windows PowerShell, and it will start downloading pretrained model (if not downloaded yet) and started training.


   After training, you can get the result image in the "result"  folder (which locates at the same directory as .py files).


   The image is named as "result\chicago_wave_gatys.jpg" or "result\chicago_wave_laps.jpg" depending on which code you run.
   

3. **Run with Customized Settings**

   1. Change the Read and Write Path

      For both models, we have "content", "style" and "save" parameters to change the default read and save path.

      You can use commands like

      ```
      python GatyStyle.py --content content_path\content_img.jpg --style style_path\style_img.jpg --save save_path\save_name.jpg
      ```

      to change the content or style image that will be used, as well as the directory and name of the result image.

   2. Choose whether use Checkpoint

       Also for both models, you can use parameter "checkpoint" to choose whether use checkpoint or not.

       The default value for "checkpoint" is 0, which means to use no checkpoint.

       If you do wish to use checkpoint, you can use command like

       ```
       python GatyStyle.py --checkpoint 1
       ```

   3.  Change the Size of Result Image

       You can use command like

       ```
       python GatyStyle.py --size 600
       ```

       and the result image will have a height of 600 pixels and the width will also change proportionally.

   4.  Change Training Parameters

       Both models have "iter","content_weight" and "style_weight" parameters.

       To change them, you can use commands like

       ```
       python GatyStyle.py --iter 6000 --content_weight 1 --style_weight 1000
       ```

       And for LapStyle model, it has an extra parameter called "lap_weight".

       To change it, you can use following command

       ```
       python LapStyle.py --lap_weight 0.5
       ```
## 3. MetaStyle

   1. **Training**

      1. Download Dataset

         Download content image dataset and style image dataset form [MS-COCO](http://cocodataset.org/#download) and [WikiArt](https://www.kaggle.com/c/painter-by-numbers).
      2. Run with Default Settings

         You can use command
         ```
         python main.py train --content-dataset <path_to_content_dataset>--style-dataset <path_to_style_dataset> --cuda 1
         ```
         to run the model with default settings.

         The path should be a folder containing another folder with all content or style images.
         Cuda 1 means using GPU while cuda 0 means using CPU.

         The trained model will be save in './experiments/save'.

      3. Run with Customized Settings

         To change directories, you can add
         ```
         --save-model-dir <your_save_path> --checkpoint-model-dir <your_checkpoint_path> --log-dir <your_log_path>
         ```
         at the end of above command.

  
   2. **Fast Training**

       1. Run with Default Settings
          
          You can use command
          ```
          python main.py fast --content-dataset <path_to_content_dataset> --style-image <path_to_style_image> --model your_model.pth --cuda 1
          ```

          The trained model will be saved in './experiments/save' as well.
       2. Run with Customized Settings

          You can change the directory of saving model by adding argument
          ```
          --save-model-dir <your_save_path>
          ```

          If you want to update only IN layers, you can add the following argument
          ```
          --only-in 1
          ``` 
         
    
   3. **Testing**

      You can use command
      ```
      python main.py test --content-image <path_to_content_img> --output_image <path_to_output image> --model your_model.pth --cuda 1
      ```
