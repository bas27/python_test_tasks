FROM python:3

WORKDIR /usr/src/app

# достоточно копирование 3 файлов(csv.py, data.tgz, requirements.txt)
COPY requirements.txt csv_sum.py data.tgz ./

#производительность: уменьшаем количество слоев, передавая выполнение команд в один RUN
#по-моему имело бы место очистка кэша apt, путем /var/lib/apt/lists его удаления уменьшается размер изображения, поскольку кэш apt не хранится в слое
#добавить аргумент -y в команду apt-get install, для исключения ручного вмешательства
#для получения точно последних версий приложений использовать RUN apt-get update с apt-get install в одном RUN, 
#- так как есть шанс при установке пакета получить устаревшую версию, из за повторного использования списка пакетов из кэша, после apt-get update 
#- чтобы не получить конкретный пакет необходимо в сборках указывать конкретную версию приложения


RUN pip install -r requirements.txt \
    && apt-get update \
    && apt-get install -y tar \
    && rm -rf /var/lib/apt/lists/* \ 
    && tar zxfv data.tgz
