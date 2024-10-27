using System;
using System.IO;
using System.IO.Compression;

namespace Archiver
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Добро пожаловать в архиватор!");
            Console.WriteLine("Выберите действие:");
            Console.WriteLine("1. Создать архив");
            Console.WriteLine("2. Распаковать архив");
            Console.WriteLine("3. Выход");

            int choice = int.Parse(Console.ReadLine());

            switch (choice)
            {
                case 1:
                    CreateArchive();
                    break;
                case 2:
                    ExtractArchive();
                    break;
                case 3:
                    Console.WriteLine("До свидания!");
                    break;
                default:
                    Console.WriteLine("Неверный выбор.");
                    break;
            }
        }

        static void CreateArchive()
        {
            Console.WriteLine("Введите путь к папке, которую нужно заархивировать:");
            string folderPath = Console.ReadLine();

            Console.WriteLine("Введите имя архива (без расширения):");
            string archiveName = Console.ReadLine();

            if (!Directory.Exists(folderPath))
            {
                Console.WriteLine("Папка не найдена.");
                return;
            }

            string archivePath = archiveName + ".zip";

            try
            {
                ZipFile.CreateFromDirectory(folderPath, archivePath);
                Console.WriteLine($"Архив {archiveName}.zip создан успешно.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Ошибка при создании архива: {ex.Message}");
            }
        }

        static void ExtractArchive()
        {
            Console.WriteLine("Введите путь к архиву:");
            string archivePath = Console.ReadLine();

            Console.WriteLine("Введите путь к папке для распаковки (или оставьте пустым, чтобы распаковать в текущую):");
            string extractPath = Console.ReadLine();

            if (!File.Exists(archivePath))
            {
                Console.WriteLine("Архив не найден.");
                return;
            }

            try
            {
                ZipFile.ExtractToDirectory(archivePath, extractPath);
                Console.WriteLine($"Архив {archivePath} распакован успешно.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Ошибка при распаковке архива: {ex.Message}");
            }
        }
    }
}
