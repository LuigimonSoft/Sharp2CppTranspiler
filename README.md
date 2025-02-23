# 🚀 Sharp2CppTranspiler

**Sharp2CppTranspiler** is a tool that automatically converts **C# Windows Forms** code into equivalent **C++** code using the **Win32 API**

This transpiler is designed for developers who want to port applications written in C# to C++, preserving the original structure, controls, events, and properties of the forms.

---

## 🔥 **Key Features**

- ✅ Automatic transpilation of classes, methods, and attributes.
- ✅ Conversion of Windows Forms controls to Win32 API:
  - `Button`, `TextBox`, `Label`, `CheckBox`, `ComboBox`, `ListBox`, `TrackBar`.
- ✅ Full support for control properties:
  - `Text`, `Size`, `Location`, `Enabled`, `Visible`, `Font`.
- ✅ Detection and conversion of events:
  - `Click`, `KeyDown`, `KeyUp`, `KeyPress`, `TextChanged`, `CheckedChanged`, `SelectedIndexChanged`, `Scroll`.
- ✅ Support for Lambda expressions (`=>`) and LINQ queries (`Where`, `Select`, `OrderBy`).
- ✅ Conversion of .NET collections:
  - `List<T>` → `std::vector<T>`
  - `Dictionary<K, V>` → `std::map<K, V>`
- ✅ Modular code following **SOLID** principles and **Clean Code** best practices.

---

## ⚙️ **Installation**

### 🔹 Prerequisites

- [.NET 6.0+ SDK](https://dotnet.microsoft.com/en-us/download)
- [C++ Compiler](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

### 🔹 Clone the repository

```bash
git clone https://github.com/luigimonsoft/Sharp2CppTranspiler.git
cd Sharp2CppTranspiler
```

### 🔹 Build the project

```bash
dotnet build
```

---

## 🚀 **Usage**

### 🔹 Transpile a file

```bash
dotnet run --project Sharp2CppTranspiler.csproj <file.cs>
```

📌 **Example:**

```bash
dotnet run --project Sharp2CppTranspiler.csproj ./src/Examples/Form1.cs
```

This will generate two files:

- `Form1.h` → Header file with class, method, and property definitions.
- `Form1.cpp` → Implementation file with the equivalent C++ code.

### 🔹 Example C# code:

```csharp
using System;
using System.Windows.Forms;

public class MyForm : Form
{
    private Button myButton;

    public MyForm()
    {
        myButton = new Button();
        myButton.Text = "Click Me!";
        myButton.Click += OnButtonClick;
        Controls.Add(myButton);
    }

    private void OnButtonClick(object sender, EventArgs e)
    {
        MessageBox.Show("Button clicked!");
    }
}
```

### 🔹 Generated C++ code:

```cpp
#include "MyForm.h"

MyForm::MyForm() {
    HWND hwnd = CreateWindow("MyWindow", "Title", WS_OVERLAPPEDWINDOW, CW_USEDEFAULT, CW_USEDEFAULT, 500, 400, NULL, NULL, GetModuleHandle(NULL), NULL);
    
    myButton = CreateWindow("BUTTON", "Click Me!", WS_CHILD | WS_VISIBLE, 50, 50, 100, 30, hwnd, NULL, GetModuleHandle(NULL), NULL);
}

LRESULT CALLBACK MyForm::OnButtonClick(HWND hwnd, UINT msg, WPARAM wParam, LPARAM lParam) {
    MessageBox(hwnd, "Button clicked!", "Event", MB_OK);
    return DefWindowProc(hwnd, msg, wParam, lParam);
}
```

---

## 🔧 **Project Structure**

```plaintext
Sharp2CppTranspiler/
│
├── src/
│   ├── Analyzers/            # Code analyzers (Roslyn)
│   ├── Generators/           # Header and implementation file generators
│   ├── Models/               # Data model definitions
│   ├── Transpiler.cs         # Main transpiler coordinator
│   ├── Program.cs            # Entry point of the application
│
├── tests/                    # Unit tests
│
├── docs/                     # Documentation and examples
│
├── README.md                 # Main documentation
├── LICENSE                   # License file
└── Sharp2CppTranspiler.sln   # Visual Studio solution
```

---

## 🛠️ **Future Configuration Options**

- 🌐 Support for `async/await` and multithreading using `std::thread`.
- 🎨 Customization of control styles (color, borders, etc.).
- 🔥 Support for `struct`, `delegate`, and `event` from C#.
- ⚡ Advanced inheritance and interface support.

---

## 💻 **Contributing**

Contributions are welcome! If you want to contribute:

1. Fork the repository.
2. Create a new branch (`git checkout -b feature/new-feature`).
3. Make your changes and commit (`git commit -am 'Add new feature'`).
4. Submit a pull request.

---

## 📄 **License**

This project is licensed under the [MIT License](./LICENSE).

---

## 🙌 **Credits**

Developed with ❤️[ by ](https://github.com/luigimonsoft)[Luigimon](https://github.com/luigimonsoft)

---

## 🚀 **Want to add more controls or improve transpilation?**

🔹 Open an issue or request a feature, and let's discuss it!

