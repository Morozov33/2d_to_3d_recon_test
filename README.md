## Результаты тестового задания по 2d-to-3d реконструкции. ##

Исходные изображения для тестирования в папке test.

## 14.08.22 ##
### [Mersh-R-CNN](https://github.com/facebookresearch/meshrcnn) ###
  Результаты в папке Mersh_R_CNN

  1. Не устанавливается на локальную машину из-за конфликта версий пакетов
  `Requirement already satisfied: torchvision>=0.4 in /opt/homebrew/lib/python3.9/site-packages (from meshrcnn==1.0) (0.13.1)
   Requirement already satisfied: fvcore in /opt/homebrew/lib/python3.9/site-packages (from meshrcnn==1.0) (0.1.5.post20220512)`
   
  2. Использовалась в среде Google Cloud
    Результаты тестов на изображении человека - неудовлетворительные (test_1.jpg, test_2.jpg). Тестирование на изображении предмета дает чуть лучшие результаты (test3.jpg).
    
### [PIFU HD](https://github.com/facebookresearch/pifuhd) ###
  Результаты в папке PIFU_HD. Использовалась в среде Google Cloud. Результаты заметно лучше, но все еще много артефактов, неполное изображение, не переносится цвет.

### [DECA](https://github.com/YadiraF/DECA) ###
  1. Не запускается на локальной машине из-за того, что используется библиотека CUDA, которая не поддерживается на macOS.
  From (https://github.com/pytorch/pytorch#installation):
  `If you want to compile with CUDA support, install the following (note that CUDA is not supported on macOS)`

  2. Пока не удалось протестировать в Google Cloud, при установки зависимостей возникают конфликты версий при установке библиотек pytorch и CUDA.
  
  3. Запустилась в Google Cloud, результаты в папке DECA - хорошо отрисовывается модель, но в демоверсии текстура переносится не полностью.
  Для переноса текстур полностью необходим файл FLAME_albedo_from_BFM.npz - конвертировал его из датасета BFM на локальной машине. Файл весит 1,26 Гб, пока не получилось загрузить его в Google Cloud из-за размера. На локальной машине не запускается DECA по прежнему из-за отсутствия поддержки CUDA (Nvidia прекратил поддержку в 2017г из-за ссоры с Apple) (??? Попробовать раннии версии).
  
### [HMR](https://github.com/akanazawa/hmr) ###
  1. Не запускается на локальной машине, при установке зависимостей pip конфликтует с библиотекой TensorFlow:
  `Configuring installation scheme with distutils config files is deprecated and will no longer work in the near future. If you are using a Homebrew or Linuxbrew Python, please see discussion at https://github.com/Homebrew/homebrew-core/issues/76621`
  
## 15.08.22 ##
### [PIFU HD](https://github.com/facebookresearch/pifuhd) ###
Результаты в папке PIFU_HD. Использовалась в среде Google Cloud. Модель хорошо отрисовывается с полноростовой фотографии, но не переносит текстуры (см. PIFU_HD/test_4_PIFU_HD_screen.png). Решение - попробовать раннюю версию библиотеки PIFU.

### [PIFU](https://github.com/shunsukesaito/PIFu) ###
  1. Ранняя версия библиотеки PIFU HD. Запускалась в Google Cloud.
  2. Качество отрисовки модели ниже, но зато переносит текстуры. Результат - PIFU/result_test_4.png.
  3. С НЕ полноростовым изображением по прежнему работает хуже, результат - PIFU/result_test_5.png.

### [DECA](https://github.com/YadiraF/DECA) ###
  3. Запустилась в Google Cloud, результаты в папке DECA - хорошо отрисовывается модель, но в демоверсии текстура переносится не полностью.
  Для переноса текстур полностью необходим файл FLAME_albedo_from_BFM.npz - конвертировал его из датасета BFM на локальной машине. Файл весит 1,26 Гб, пока не получилось загрузить его в Google Cloud из-за размера. На локальной машине не запускается DECA по прежнему из-за отсутствия поддержки CUDA (Nvidia прекратил поддержку в 2017г из-за ссоры с Apple) (??? Попробовать раннии версии).
 
## 16.08.22 ##
### 1. Прочитано Readme к библиотекам: ###
1. [SynergyNet](https://github.com/choyingw/SynergyNet)
2. [Deep3DFaceReconstruction](https://github.com/microsoft/Deep3DFaceReconstruction)
3. [DAD-3DHeads](https://github.com/PinataFarms/DAD-3DHeads)
4. [eos](https://github.com/patrikhuber/eos)
5. [extreme_3d_faces](https://github.com/anhttran/extreme_3d_faces)
6. [NextFace](https://github.com/abdallahdib/NextFace)
7. [3DMM-Fitting-Pytorch](https://github.com/ascust/3DMM-Fitting-Pytorch)
8. [GANFit](https://github.com/barisgecer/GANFit)

Большинство этих моделей либо основаны на DECA и не превосходят ее по параметрам. Так же многие модели используют CUDA, что делает невозможным запуск на локальной машине под MacOS.

### 2. Продолжается работа с библиотекой DECA ###
В Google Cloud добавлена FLAME модель FLAME_albedo_from_BFM.npz. Результаты ее использования - файлы [result_test_5_DECA_16.08.22.png](https://github.com/Morozov33/2d_to_3d_recon_test/blob/main/DECA/result_test_5_DECA_16.08.22.png) и [result_test_6_DECA_16.08.22.png](https://github.com/Morozov33/2d_to_3d_recon_test/blob/main/DECA/result_test_6_DECA_16.08.22.png).
Результаты не сильно отличаются от обычной версии DECA. Возможно это связанно с предупреждениями, возникающими при моделировании:

`/usr/local/lib/python3.7/dist-packages/torch/nn/functional.py:3121: UserWarning: Default upsampling behavior when mode=bilinear is changed to align_corners=False since 0.4.0. Please specify align_corners=True if the old behavior is desired. See the documentation of nn.Upsample for details. "See the documentation of nn.Upsample for details.".format(mode))`

`/content/DECA/decalib/deca.py:128: UserWarning: Mixed memory format inputs detected while calling the operator. The operator will output channels_last tensor even if some of the inputs are not in channels_last format. (Triggered internally at  /pytorch/aten/src/ATen/native/TensorIterator.cpp:924.)
 uv_detail_normals = uv_detail_normals*self.uv_face_eye_mask + uv_coarse_normals*(1.-self.uv_face_eye_mask)`
 
`/content/DECA/decalib/utils/renderer.py:280: UserWarning: Mixed memory format inputs detected while calling the operator. The operator will output contiguous tensor even if some of the inputs are in channels_last format. (Triggered internally at  /pytorch/aten/src/ATen/native/TensorIterator.cpp:918.)
  images = images*alpha_images + background*(1.-alpha_images`

## 17.08.22 ##
### 1. [Deep3DFaceReconstruction](https://github.com/microsoft/Deep3DFaceReconstruction) ###
Поддерживает Linux и Windows, значит не получится запустить на локалльной машине.

### 2. DECA ###
Результаты: [result_test_5_DECA_17.08.22.png](https://github.com/Morozov33/2d_to_3d_recon_test/blob/main/DECA/result_test_5_DECA_17.08.22.png) и [result_test_6_DECA_17.08.22.png](https://github.com/Morozov33/2d_to_3d_recon_test/blob/main/DECA/result_test_6_DECA_17.08.22.png). Использование модели FLAME не дает полной отрисовки текстур, как в демо-примере от разработчиков. В чем кроется причина - не понятно, написал issue к разработчикам. 

## 19.08.22 ##
### DECA ###
Удалось полностью перенести текстуру на 3D модель с помощью модели FLAME выполняя код в Google Cloud. Результаты: [result_test_5_DECA_19.08.22.png](https://github.com/Morozov33/2d_to_3d_recon_test/blob/main/DECA/result_test_5_DECA_19.08.22.png) и [result_test_6_DECA_19.08.22.png](https://github.com/Morozov33/2d_to_3d_recon_test/blob/main/DECA/result_test_6_DECA_19.08.22.png).
Качество не очень высокое (связанно ли это с качеством исходного изображения?), а так же не отрисовывается прическа (задать вопрос разработчикам).
