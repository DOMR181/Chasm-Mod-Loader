# CHASM Mod Loader

<p align="center">
  <img src="CHASM_Mod loader.jpg" alt="CHASM Mod Loader Logo" width="600">
</p>

**CHASM** — это легковесный, экспериментальный загрузчик модов для Minecraft 1.20.1, работающий напрямую через Java Instrumentation API (`-javaagent`). 

> *"Никакого Фабрика, только чистый код!"*

---

## 🚀 Особенности (Features)
* **Чистый Java Agent:** Внедряется прямо в рантайм Mojang до старта основного игрового движка.
* **Динамическая загрузка:** Сканирует папку `chasm_mods` и загружает внешние `.jar` файлы на лету через кастомный `URLClassLoader`.
* **Асинхронность:** Безопасный фоновый поток для кастомизации игрового окна без конфликтов с графической библиотекой GLFW.

---

## 🛠️ Как это работает?

Лоадер перехватывает управление при запуске игры, подготавливает среду и ищет в папке `chasm_mods` скомпилированные дополнения. Лоадер ожидает, что у каждого мода есть главный класс-вход по пути `ru.mycustommod.ModInit` с методом `start()`.

---

## 📦 Установка и запуск (в Prism Launcher)

1. Скачайте актуальный `ChasmLoader-1.0-SNAPSHOT.jar`.
2. В Prism Launcher зайдите в настройки вашей папки (инстанса) Minecraft 1.20.1.
3. Перейдите во вкладку **"Параметры Java"** -> **"Аргументы Java"** и добавьте аргумент запуска:
   ```text
   -javaagent:Пут_К_Вашему_Файлу/ChasmLoader-1.0-SNAPSHOT.jar

📝 Пример создания мода (FPS Counter Mod)
Чтобы лоадер успешно распознал ваш мод, создайте структуру пакетов ru.mycustommod, класс ModInit и метод start():

Java
package ru.mycustommod;

public class ModInit {
    public static void start() {
        System.out.println("[MyMod] Привет из бездны через CHASM!");
        
        // Ваш код мода (например, счетчик FPS в фоне)
        Thread thread = new Thread(() -> {
            while (true) {
                try {
                    Thread.sleep(1000);
                    // Логика опроса Minecraft через рефлексию...
                } catch (Exception e) {
                    e.printStackTrace();
                }
            }
        });
        thread.setDaemon(true);
        thread.start();
    }
}
📄 Лицензия
Этот проект распространяется под лицензией MIT License — вы можете свободно использовать, изменять и распространять этот код.


---
