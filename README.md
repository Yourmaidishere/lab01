Скачала архив через команду
* wget https://sourceforge.net/projects/boost/files/boost/1.69.0/boost_1_69_0.tar.gz

В терминале отображается процесс скачивания

Следующей командой
* tar -xf boost_1_69_0.tar.gz

Распаковала архив

Потом я перешла в только что созданную папку через команду
* cd boost_1_69_0/

Считала файлы командой find(находит все удовлетворяющие требованиям файлы). И результат работы данной команды я перенаправляла на команду wc, которая считает колличество входящих строк, слов и символов. Мне нужно только первое число
При вводе команды
*  find ./ -maxdepth 1 | wc

я получаю результат 
* 19 19 209

но первая строчка вывода была пустой, она не учитывалась, поэтому 19-1 = 18 файлов в данной папке
Теперь посчитаем все файлы: для этого уберем оператор maxdepth, который ограничивает глубину сканирования
* find ./ | wc

на выходе получаем:
* 66829   66832 3286648

66829 - 1 = 66828 файлов всего
Дальше подсчитаем файлы с различными расширениями
* find ./ -name "*.h" |wc
* find ./ -name "*.cpp" |wc

На выходе получаем следующие значения:
- 296     296   11738
- 13774   13774  647953

66828 - 296 - 13774 = 52758 оставшихся файлов
Дальше нам требуется найти файл any.hpp команды те же:
* find ./ -name "any.hpp"

Получаем список файлов с таким же названием, нам нужен только первый
- ./boost/any.hpp

Но нам нужен полный путь до этого файла. Для этого в начало допишем путь к нашей директории:
- ~/Mainyourhere/workspace/boost_1_69_0/boost/any.hpp

Поиск внутри файлов делаю с помощью команды grep:
* grep -r "boost::asio" ./

Получаю очень много файлов
Дальше компилируем, как было сказано на сайте:
* ./bootstrap.sh --prefix=boost_output
* ./b2 install

После завершенния компиляции мы переносим скомпилированные файлы в нужную директорию
* mkdir ~/boost-libs
* mv boost_output/ ~/boost-libs/

После чего мы переходим в неё
* cd ~/boost_libs 

Мне нужно найти 10 самых тяжелых файлов, сделать я это могу с помощью команды: 
* find . -type f -exec ls -s {} \; | sort -n | head -10

С помощью команды find я нахожу все файлы в данной директории.
С помощью опции -exec я каждый найденый файл перенаправляю в команду ls, которая с помощью опции -с выводит нам размер файла
Команда sort -n сортирует переданный ей список файлов по первому числу, а это как раз размер и передает результат дальше.
Команда head -10 выводит нам только 10 первых пунктов переданных ей на вход данных.
* ./boost_out/include/boost/accumulators/accumulators.hpp
* ./boost_out/include/boost/accumulators/framework/accumulator_base.hpp
* ./boost_out/include/boost/accumulators/framework/accumulator_concept.hpp
* ./boost_out/include/boost/accumulators/framework/accumulators/external_accumulator.hpp
* ./boost_out/include/boost/accumulators/framework/accumulators/reference_accumulator.hpp
* ./boost_out/include/boost/accumulators/framework/accumulators/value_accumulator.hpp
* ./boost_out/include/boost/accumulators/framework/external.hpp
* ./boost_out/include/boost/accumulators/framework/features.hpp
* ./boost_out/include/boost/accumulators/framework/parameters/accumulator.hpp
* ./boost_out/include/boost/accumulators/framework/parameters/sample.hpp
