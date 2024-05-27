# tmp_tmp
Показ диаграмм и кусок программы

Диаграмма классов:
![image](https://github.com/Fellmonkey/tmp_tmp/assets/90258055/dd3bce62-cc60-4a4a-a3d7-8e59926fdf20)

Блок-схема программы:
![mermaid-diagram-2024-05-27-153619](https://github.com/Fellmonkey/tmp_tmp/assets/90258055/fb74a2b4-fd11-4fe6-9b0d-8dd1b7c7c5ed)

Логическая структруа программы:
![image](https://github.com/Fellmonkey/tmp_tmp/assets/90258055/0ad5a366-0b9b-4ea3-9a3b-a843e951e3a3)
Программа работает по следующему принципу : существует класс-интерфейс IMicrophone, от которого методом одиночного наследования создаются производные классы Microphone, от Microphone  создаются производные классы WiredMicrophone и WirelessMicrophone, также WirelessMicrophone наследуется от AudioReceiver, от WiredMicrophone создаются производные классы DynamicMicrophone и CondenserMicrophone. Объекты таких производных классов помещаются в контейнерный шаблонный класса DynamicVector, а адреса на эти объекты помещаются в  vector указателей на void, который хранит объект класса GenericContainer.
Также контейнер, предназначенный для хранения объектов, DynamicVector имеет возможность запись объектов в файл путём вызова метода save(string path). Соответственно таких файлов 5(default.txt, wired.txt, wireless.txt, dynamic.txt, condenser.txt). Ещё DynamicVector поддерживает чтение этих файлов объектов и занесения их в контейнер объектов c помощью метода load(string path).

Модульная структура программы:
![image](https://github.com/Fellmonkey/tmp_tmp/assets/90258055/751524b6-3c25-471b-9657-c0a990492c15)

Код главной части:
```C++
#include "CondenserMicrophone.h"
#include "PtrClassTemplate.h"
#include "DynamicMicrophone.h"
#include "DynamicVector.h"
#include "WiredMicrophone.h"
#include "WirelessMicrophone.h"
#include <windows.h>
using namespace std;
using namespace kurs;

template <typename T1, typename T2>
void Message(T1 message1, T2 message2)
{
    cout << message1 << message2 << endl;
}
void SetColor(WORD text, WORD background)
{
    const HANDLE h_console_handle = GetStdHandle(STD_OUTPUT_HANDLE);
    SetConsoleTextAttribute(h_console_handle, text | background);
}
void info()
{
    //create
    SetColor(FOREGROUND_BLUE, NULL);
    Message("Section ", "\"Create\"");
    SetColor(15,NULL);
    Message("Print \"create dynamic\"", " to create mic");
    Message("Print \"create condenser\"", " to create mic");
    Message("Print \"create wired\"", " to create mic");
    Message("Print \"create wireless\"", " to create mic");
    Message("Print \"create default\"", " to create any mic");
    //print
    SetColor(FOREGROUND_GREEN, NULL);
    Message("Section ", "\"Print\"");
    SetColor(15,NULL);
    Message("Print \"print dynamic\"", " to print all mic this class");
    Message("Print \"print condenser\"", " to print all mic this class");
    Message("Print \"print wired\"", " to print all mic this class");
    Message("Print \"print wireless\"", " to print all mic this class");
    Message("Print \"print defalut\"", " to print all mic this class");
    Message("Print \"print ptr\"", " to print all mic");
    //clear
    SetColor(FOREGROUND_RED, NULL);
    Message("Section ", "\"Clear\"");
    SetColor(15,NULL);
    Message("Print \"clear all\"", " to clear all mic all class");
    //load
    SetColor(14, NULL);
    Message("Section ", "\"Load\"");
    SetColor(15,NULL);
    Message("Print \"load all\"", " to load information about each class container to a file");

    //save
    SetColor(FOREGROUND_GREEN, NULL);
    Message("Section ", "\"Save\"");
    SetColor(15,NULL);
    Message("Print \"save all\"", " to save information about each class container to a file");
    //stop
    SetColor(4, NULL);
    Message("Print ", "\"stop\" to close program");
    SetColor(15,NULL);
    //sort
    SetColor(6, NULL);
    Message("Section ", "\"Sort\"");
    SetColor(15,NULL);
    Message("Print \"sort by name ptr\"", " to sort all mic in ptr container");
    Message("Print \"sort by price ptr\"", " to sort all mic in ptr container");
    Message("Print \"sort by name\"", " to sort all mic in all container");
    Message("Print \"sort by price\"", " to sort all mic in all container");
}

template <typename MicrophoneType>
void create_microphone(DynamicVector<MicrophoneType>& container, PtrClassTemplate<IMicrophone>& ptr_container) {

    MicrophoneType microphone;
    microphone.set_all();
    container.push_back(microphone);

   // ptr_container.add(&container[container.get_size()-1]);
}
int main()
{
    string command;
    DynamicVector<DynamicMicrophone> vdynamic_mic;
    DynamicVector<CondenserMicrophone> vcondenser_mic;
    DynamicVector<WiredMicrophone> vwired_mic;
    DynamicVector<WirelessMicrophone> vwireless_mic;
    DynamicVector<Microphone> v_mic;


    PtrClassTemplate<IMicrophone> ptr_container;
    Message("Print \"help\" to info", "");
    while (true)
    {
        getline(cin,command);
        if(command.empty()) continue;
        if(command == "help")
        {
            info();
        }
        else if(command == "create dynamic")
        {
            create_microphone(vdynamic_mic,ptr_container);
        }else if(command == "create condenser")
        {
            create_microphone(vcondenser_mic,ptr_container);
        }else if(command == "create wired")
        {
            create_microphone(vwired_mic,ptr_container);
        }else if(command == "create wireless")
        {
            create_microphone(vwireless_mic,ptr_container);
        }else if(command == "create default")
        {
            create_microphone(v_mic,ptr_container);
        }
        else if(command == "print dynamic")
        {
            Message("Print Dynamic mic", "");
            vdynamic_mic.print();
        }else if(command == "print condenser")
        {
            Message("Print Condenser mic", "");
            vcondenser_mic.print();
        }else if(command == "print wired")
        {
            Message("Print Wired mic", "");
            vwired_mic.print();
        }else if(command == "print wireless")
        {
            Message("Print Wireless mic", "");
            vwireless_mic.print();
        }else if(command == "print default")
        {
            Message("Print default mic", "");
            v_mic.print();
        }
        else if(command == "print ptr")
        {
            Message("Print all object in ptr container", "");
            ptr_container.display_all();
        }
        else if(command == "clear all")
        {
            v_mic.clear();
            vcondenser_mic.clear();
            vdynamic_mic.clear();
            vwired_mic.clear();
            vwireless_mic.clear();
            ptr_container.clear();
            Message("Success clear", "");
        }
        else if(command == "load all")
        {
            v_mic.load("default.txt");
            vcondenser_mic.load("condenser.txt");
            vdynamic_mic.load("dynamic.txt");
            vwired_mic.load("wired.txt");
            vwireless_mic.load("wireless.txt");
        }
        else if(command == "save all")
        {
            v_mic.save("default.txt");
            vcondenser_mic.save("condenser.txt");
            vdynamic_mic.save("dynamic.txt");
            vwired_mic.save("wired.txt");
            vwireless_mic.save("wireless.txt");
        }
        else if(command == "stop")
        {
            break;
        }
        else if(command == "sort by name ptr")
        {
            ptr_container.sort_by_name();
            Message("Success sort by name", "");
        }else if(command == "sort by price ptr")
        {
            ptr_container.sort_by_price();
            Message("Success sort by price", "");
        }else if(command == "sort by name")
        {
            v_mic.sort_by_name_h();
            vcondenser_mic.sort_by_name_h();
            vdynamic_mic.sort_by_name_h();
            vwired_mic.sort_by_name_h();
            vwireless_mic.sort_by_name_h();
            Message("Success sort by name", "");
        }else if(command == "sort by price")
        {
            v_mic.sort_by_price_h();
            vcondenser_mic.sort_by_price_h();
            vdynamic_mic.sort_by_price_h();
            vwired_mic.sort_by_price_h();
            vwireless_mic.sort_by_price_h();
            Message("Success sort by price", "");
        }
        else
        {
            Message("Unknown command\n", "Try again");
        }
    }
}

```
