## Результаты тестового задания по 2d-to-3d реконструкции. ##

Изображения для тестирования в папке test

Использованные библиотеки:
### 1. Mersh-R-CNN[](https://github.com/facebookresearch/meshrcnn) ###
  Результаты в папке Mersh_R_CNN

  1. Не устанавливается на локальную машину из-за конфликта версий пакетов
  `Requirement already satisfied: torchvision>=0.4 in /opt/homebrew/lib/python3.9/site-packages (from meshrcnn==1.0) (0.13.1)
   Requirement already satisfied: fvcore in /opt/homebrew/lib/python3.9/site-packages (from meshrcnn==1.0) (0.1.5.post20220512)`
   
  2. Использовалась в среде Google Cloud
    Результаты тестов на изображении человека - неудовлетворительные (test_1.jpg, test_2.jpg). Тестирование на изображении предмета дает чуть лучшие результаты (test3.jpg).
    
### 2. [PIFU HD](https://github.com/facebookresearch/pifuhd) ###
  Результаты в папке PIFU_HD. Использовалась в среде Google Cloud. Результаты заметно лучше, но все еще много артефактов, неполное изображение, не переносится цвет.

### 3. [DECA](https://github.com/YadiraF/DECA) ###
  1. Не запускается на локальной машине из-за того, что используется библиотека CUDA, которая не поддерживается на macOS.
  2. Пока не удалось протестировать в Google Cloud, при установки зависимостей возникают конфликты версий при установке библиотек pytorch и CUDA.
  
  
### 4. [HMR](https://github.com/akanazawa/hmr) ###
  1. Не запускается на локальной машине, при установке зависимостей pip конфликтует с библиотекой TensorFlow:
  `Configuring installation scheme with distutils config files is deprecated and will no longer work in the near future. If you are using a Homebrew or Linuxbrew Python, please see discussion at https://github.com/Homebrew/homebrew-core/issues/76621`
