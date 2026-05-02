# Отчёт по лабораторной работе №10
## Программирование в командном процессоре ОС UNIX

**Студент:** [Введите ваше ФИО]

**Цель работы:** Изучение основ программирования в командной оболочке bash, приобретение навыков написания скриптов для автоматизации задач администрирования и обработки файлов в ОС UNIX/Linux.

---

## Задание №1. Резервное копирование скрипта

**Краткое описание:** Создан скрипт, который при запуске создаёт резервную копию своего исходного кода. Копия сохраняется в директории `~/backup` с использованием архиватора tar и метки времени в имени файла.

**Листинг кода:**
```bash
#!/bin/bash

# Création du répertoire backup dans le home s'il n'existe pas
BACKUP_DIR="$HOME/backup"
mkdir -p "$BACKUP_DIR"

# Nom du script actuel (fichier en cours d'exécution)
SCRIPT_NAME="$0"

# Vérification que le script existe
if [ ! -f "$SCRIPT_NAME" ]; then
    echo "Erreur : Le fichier source n'existe pas."
    exit 1
fi

# Nom du fichier de sauvegarde avec horodatage
DATE=$(date +"%Y%m%d_%H%M%S")
BACKUP_FILE="$BACKUP_DIR/script_backup_$DATE.tar.gz"

# Compression avec tar (gzip)
tar -czf "$BACKUP_FILE" "$SCRIPT_NAME"

echo "Sauvegarde effectuée avec succès : $BACKUP_FILE"
ls -lh "$BACKUP_FILE"
