## Результаты тестового задания по 2d-to-3d реконструкции. ##

Изображения для тестирования в папке test.

Использованные библиотеки:
### 1. [Mersh-R-CNN](https://github.com/facebookresearch/meshrcnn) ###
  Результаты в папке Mersh_R_CNN

  1. Не устанавливается на локальную машину из-за конфликта версий пакетов
  `Requirement already satisfied: torchvision>=0.4 in /opt/homebrew/lib/python3.9/site-packages (from meshrcnn==1.0) (0.13.1)
   Requirement already satisfied: fvcore in /opt/homebrew/lib/python3.9/site-packages (from meshrcnn==1.0) (0.1.5.post20220512)`
   
  2. Использовалась в среде Google Cloud
    Результаты тестов на изображении человека - неудовлетворительные (test_1.jpg, test_2.jpg). Тестирование на изображении предмета дает чуть лучшие результаты (test3.jpg).
    
### 2. [PIFU HD](https://github.com/facebookresearch/pifuhd) ###
  Результаты в папке PIFU_HD. Использовалась в среде Google Cloud. Результаты заметно лучше, но все еще много артефактов, неполное изображение, не переносится цвет.
  2.1. Модель хорошо отрисовывается с полноростовой фотографии, но не переносит текстуры (см. PIFU_HD/test_4_PIFU_HD_screen.png). Решение - попробовать раннюю версию библиотеки PIFU - см. пункт 5.

### 3. [DECA](https://github.com/YadiraF/DECA) ###
  1. Не запускается на локальной машине из-за того, что используется библиотека CUDA, которая не поддерживается на macOS.
  From (https://github.com/pytorch/pytorch#installation):
  `If you want to compile with CUDA support, install the following (note that CUDA is not supported on macOS)`

  2. Пока не удалось протестировать в Google Cloud, при установки зависимостей возникают конфликты версий при установке библиотек pytorch и CUDA.
  
  3. Запустилась в Google Cloud, результаты в папке DECA - хорошо отрисовывается модель, но в демоверсии текстура переносится не полностью.
  Для переноса текстур полностью необходим файл FLAME_albedo_from_BFM.npz - конвертировал его из датасета BFM на локальной машине. Файл весит 1,26 Гб, пока не получилось загрузить его в Google Cloud из-за размера. На локальной машине не запускается DECA по прежнему из-за отсутствия поддержки CUDA (Nvidia прекратил поддержку в 2017г из-за ссоры с Apple).
  
  
### 4. [HMR](https://github.com/akanazawa/hmr) ###
  1. Не запускается на локальной машине, при установке зависимостей pip конфликтует с библиотекой TensorFlow:
  `Configuring installation scheme with distutils config files is deprecated and will no longer work in the near future. If you are using a Homebrew or Linuxbrew Python, please see discussion at https://github.com/Homebrew/homebrew-core/issues/76621`
  
### 5. PIFU ###
  1. Ранняя версия библиотеки PIFU
  2. Качество отрисовки модели ниже, но зато переносит текстуры. Результат - PIFU/result_test_4.png.
  3. С НЕ полноростовым изображением по прежнему работает хуже, результат - PIFU/result_test_5.png

*to be continued...*
