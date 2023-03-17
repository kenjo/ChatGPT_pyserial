# Finding Available Serial Ports.

**Human:**
how to find out names of devices that can be used in pyserial serial.Serial() function. that works for booth winfows and linux 

***

**Assistant:**

In order to find out the names of devices that can be used in `pyserial`'s `serial.Serial()` function that works for both Windows and Linux, you can use the following steps:

1. First, import the `serial` module from the `pyserial` library:


```
import serial

```
<ol start="2">Then, use the `serial.tools.list_ports.comports()` function to get a list of available serial ports on your system. This function returns a list of `serial.tools.list_ports.ListPortInfo` objects, which contain information about each available port:</li></ol>
```
available_ports = serial.tools.list_ports.comports()

```
<ol start="3">Finally, you can iterate through the list of available ports and print out the name of each port:</li></ol>
```
for port in available_ports:
    print(port.name)

```

This code will print out the names of all available serial ports on your system, which can be used as arguments to the `serial.Serial()` function. Note that the names of the ports will be different depending on your operating system and the devices connected to your system.


***

**Human:**
write a python gui program that works on both linux and windows that opens a windows listing the available serial ports and allows the user to select one then open a new window reading from that port and displaying it in the new window

***

**Assistant:**

Sure! Here's an example Python GUI program using the `tkinter` library that works on both Linux and Windows, which lists the available serial ports, allows the user to select one, and then opens a new window to read from that port and display the data:

```
import serial.tools.list_ports
import tkinter as tk
import tkinter.scrolledtext as tkst

class SerialReaderGUI:
    def __init__(self, master):
        self.master = master
        self.master.title("Serial Reader")
        self.available_ports = self.list_available_ports()
        self.selected_port = tk.StringVar()
        self.create_widgets()

    def list_available_ports(self):
        return [port.name for port in serial.tools.list_ports.comports()]

    def create_widgets(self):
        # Create a dropdown list of available serial ports
        tk.Label(self.master, text="Select a serial port:").grid(row=0, column=0, padx=5, pady=5)
        port_dropdown = tk.OptionMenu(self.master, self.selected_port, *self.available_ports)
        port_dropdown.grid(row=0, column=1, padx=5, pady=5)

        # Create a button to open the selected serial port
        tk.Button(self.master, text="Open Port", command=self.open_serial_port).grid(row=1, column=0, columnspan=2, padx=5, pady=5)

    def open_serial_port(self):
        # Open a new window to display the data from the selected serial port
        serial_window = tk.Toplevel(self.master)
        serial_window.title("Serial Data")
        serial_window.geometry("400x400")
        tkst.ScrolledText(serial_window).pack(expand=True, fill="both")

        # Read from the selected serial port and display the data in the new window
        with serial.Serial(self.selected_port.get(), 9600) as ser:
            while True:
                line = ser.readline().decode('utf-8')
                serial_window.children['!scrolledtext'].insert(tk.END, line)

if __name__ == "__main__":
    root = tk.Tk()
    app = SerialReaderGUI(root)
    root.mainloop()

```

This program creates a GUI with a dropdown list of available serial ports and a button to open the selected port. When the button is clicked, a new window is opened to display the data from the selected serial port. The program reads data from the selected serial port using the `serial` library and displays it in the new window using the `tkinter.scrolledtext` widget.

Note that this program assumes that the serial port is transmitting data in UTF-8 encoding at a baud rate of 9600. You may need to modify the program to match the specifics of your own use case.


***

**Human:**
what is the way to install pyserial on ubuntu 

***

**Assistant:**

To install `pyserial` on Ubuntu, you can use the following steps:

1. 
Open a terminal window on your Ubuntu system.

2. 
Install `pip`, the package installer for Python, if it is not already installed. You can do this by running the following command:
<pre><div class="bg-black rounded-md mb-4"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>csharp</span><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4 overflow-y-auto"><code class="!whitespace-pre hljs language-csharp p-4">sudo apt-<span class="hljs-keyword">get</span> install python3-pip
`</code></div></div></pre><code class="!whitespace-pre hljs language-csharp p-4">
This command installs `pip` for Python 3, which is the version of Python that is installed by default on Ubuntu 20.04 and later.
</code>
3. <code class="!whitespace-pre hljs language-csharp p-4">
Install `pyserial` using `pip` by running the following command:
<pre><div class="bg-black rounded-md mb-4"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans justify-between rounded-t-md"><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4 overflow-y-auto"><code class="!whitespace-pre hljs p-4">pip3 install pyserial
`</code></div></div></pre><code class="!whitespace-pre hljs p-4">
This command installs the latest version of `pyserial` available on the Python Package Index (PyPI) for Python 3.
</code></code>
4. <code class="!whitespace-pre hljs language-csharp p-4"><code class="!whitespace-pre hljs p-4">
After the installation is complete, you can verify that `pyserial` is installed correctly by importing it in a Python script or in a Python interpreter:
<pre><div class="bg-black rounded-md mb-4"><div class="flex items-center relative text-gray-200 bg-gray-800 px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>python</span><button class="flex ml-auto gap-2"><svg stroke="currentColor" fill="none" stroke-width="2" viewBox="0 0 24 24" stroke-linecap="round" stroke-linejoin="round" class="h-4 w-4" height="1em" width="1em" xmlns="http://www.w3.org/2000/svg"><path d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2"></path><rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect></svg>Copy code</button></div><div class="p-4 overflow-y-auto"><code class="!whitespace-pre hljs language-python p-4"><span class="hljs-keyword">import</span> serial
`</code></div></div></pre><code class="!whitespace-pre hljs language-python p-4">
If no errors are raised, `pyserial` is installed correctly.
</code></code></code>


That's it! Now you should be able to use `pyserial` in your Python scripts or programs on your Ubuntu system.


***

**Human:**
make it possible to have two serial port windows at the same time 

***

**Assistant:**

To make it possible to have two serial port windows open at the same time, you can modify the `SerialReaderGUI` class in the previous code example to create a new instance of the `SerialWindow` class for each selected serial port.

Here's an example implementation:

```
import serial.tools.list_ports
import tkinter as tk
import tkinter.scrolledtext as tkst

class SerialWindow:
    def __init__(self, port):
        self.port = port
        self.window = tk.Toplevel()
        self.window.title(f"Serial Port: {self.port}")
        self.text_area = tkst.ScrolledText(self.window)
        self.text_area.pack(expand=True, fill="both")
        self.open_serial_port()

    def open_serial_port(self):
        with serial.Serial(self.port, 9600) as ser:
            while True:
                line = ser.readline().decode('utf-8')
                self.text_area.insert(tk.END, line)

class SerialReaderGUI:
    def __init__(self, master):
        self.master = master
        self.master.title("Serial Reader")
        self.available_ports = self.list_available_ports()
        self.selected_ports = []
        self.create_widgets()

    def list_available_ports(self):
        return [port.name for port in serial.tools.list_ports.comports()]

    def create_widgets(self):
        # Create a dropdown list of available serial ports
        tk.Label(self.master, text="Select a serial port:").grid(row=0, column=0, padx=5, pady=5)
        self.port_dropdown = tk.OptionMenu(self.master, tk.StringVar(), *self.available_ports)
        self.port_dropdown.grid(row=0, column=1, padx=5, pady=5)

        # Create a button to add the selected serial port
        tk.Button(self.master, text="Add Port", command=self.add_serial_port).grid(row=0, column=2, padx=5, pady=5)

    def add_serial_port(self):
        # Add a new serial window for the selected port
        port = self.port_dropdown.cget("text")
        if port not in self.selected_ports:
            self.selected_ports.append(port)
            SerialWindow(port)

if __name__ == "__main__":
    root = tk.Tk()
    app = SerialReaderGUI(root)
    root.mainloop()

```

In this modified implementation, the `SerialReaderGUI` class maintains a list of selected serial ports and creates a new instance of the `SerialWindow` class for each selected port when the "Add Port" button is clicked. The `SerialWindow` class creates a new window to display the data from the selected serial port and reads data from the port using the `serial` library.

Note that this implementation assumes that the serial port is transmitting data in UTF-8 encoding at a baud rate of 9600. You may need to modify the implementation to match the specifics of your own use case.


***

**Human:**
there is an error when using the port its the device that needs to be use dnot the name. the name is needed for the selection but device is needed to open it

***

**Assistant:**

Thank you for letting me know. You are correct that the `SerialWindow` class should use the device identifier, rather than the name, to open the serial port.

Here's a modified implementation that uses the device identifier instead of the name:

```
import serial.tools.list_ports
import tkinter as tk
import tkinter.scrolledtext as tkst

class SerialWindow:
    def __init__(self, device):
        self.device = device
        self.window = tk.Toplevel()
        self.window.title(f"Serial Port: {self.device}")
        self.text_area = tkst.ScrolledText(self.window)
        self.text_area.pack(expand=True, fill="both")
        self.open_serial_port()

    def open_serial_port(self):
        with serial.Serial(self.device, 9600) as ser:
            while True:
                line = ser.readline().decode('utf-8')
                self.text_area.insert(tk.END, line)

class SerialReaderGUI:
    def __init__(self, master):
        self.master = master
        self.master.title("Serial Reader")
        self.available_ports = self.list_available_ports()
        self.selected_devices = []
        self.create_widgets()

    def list_available_ports(self):
        return [port.device for port in serial.tools.list_ports.comports()]

    def create_widgets(self):
        # Create a dropdown list of available serial ports
        tk.Label(self.master, text="Select a serial port:").grid(row=0, column=0, padx=5, pady=5)
        self.port_dropdown = tk.OptionMenu(self.master, tk.StringVar(), *self.available_ports)
        self.port_dropdown.grid(row=0, column=1, padx=5, pady=5)

        # Create a button to add the selected serial port
        tk.Button(self.master, text="Add Port", command=self.add_serial_port).grid(row=0, column=2, padx=5, pady=5)

    def add_serial_port(self):
        # Add a new serial window for the selected port
        device = self.port_dropdown.cget("text")
        if device not in self.selected_devices:
            self.selected_devices.append(device)
            SerialWindow(device)

if __name__ == "__main__":
    root = tk.Tk()
    app = SerialReaderGUI(root)
    root.mainloop()

```

In this modified implementation, the `SerialWindow` class uses the `device` attribute instead of the `port` attribute to open the serial port. The `SerialReaderGUI` class also uses the `device` attribute to create the list of available ports and to retrieve the selected port when the "Add Port" button is clicked.


***

**Human:**
we need to read one line at a time as a read from serial port will never finish unless its removed. also I need it in 115200 speed

***

**Assistant:**

Thank you for letting me know. To read one line at a time from the serial port and set the speed to 115200, you can modify the `SerialWindow` class as follows:

```
class SerialWindow:
    def __init__(self, device):
        self.device = device
        self.window = tk.Toplevel()
        self.window.title(f"Serial Port: {self.device}")
        self.text_area = tkst.ScrolledText(self.window)
        self.text_area.pack(expand=True, fill="both")
        self.open_serial_port()

    def open_serial_port(self):
        with serial.Serial(self.device, 115200, timeout=1) as ser:
            while True:
                line = ser.readline().decode('utf-8')
                if line:
                    self.text_area.insert(tk.END, line)

```

In this modified implementation, the `SerialWindow` class uses the `timeout` parameter to wait for up to 1 second for a line of data to be received from the serial port. Once a line is received, it is added to the text area using the `insert` method. The `Serial` object is created with a baud rate of 115200, as requested.


***

**Human:**
the open_serial_port can not be part of the __init_ function as its an infinite loop. the window needs to be opend then filled in with data from readline

***

**Assistant:**

You are correct, thank you for pointing that out. The `open_serial_port` function should not be part of the `__init__` function, as it would cause the program to hang indefinitely. Instead, the `open_serial_port` function can be called after the window is created, and the text area can be updated with the data received from `readline`.

Here is the modified implementation that opens the window first and updates the text area with the data received from `readline`:

```
import serial.tools.list_ports
import tkinter as tk
import tkinter.scrolledtext as tkst
import threading

class SerialWindow:
    def __init__(self, device):
        self.device = device
        self.window = tk.Toplevel()
        self.window.title(f"Serial Port: {self.device}")
        self.text_area = tkst.ScrolledText(self.window)
        self.text_area.pack(expand=True, fill="both")
        self.start_reading()

    def start_reading(self):
        self.serial_thread = threading.Thread(target=self.read_serial_port)
        self.serial_thread.daemon = True
        self.serial_thread.start()

    def read_serial_port(self):
        with serial.Serial(self.device, 115200, timeout=1) as ser:
            while True:
                line = ser.readline().decode('utf-8')
                if line:
                    self.text_area.insert(tk.END, line)
                    self.text_area.see(tk.END)

class SerialReaderGUI:
    def __init__(self, master):
        self.master = master
        self.master.title("Serial Reader")
        self.available_ports = self.list_available_ports()
        self.selected_devices = []
        self.create_widgets()

    def list_available_ports(self):
        return [port.device for port in serial.tools.list_ports.comports()]

    def create_widgets(self):
        # Create a dropdown list of available serial ports
        tk.Label(self.master, text="Select a serial port:").grid(row=0, column=0, padx=5, pady=5)
        self.port_dropdown = tk.OptionMenu(self.master, tk.StringVar(), *self.available_ports)
        self.port_dropdown.grid(row=0, column=1, padx=5, pady=5)

        # Create a button to add the selected serial port
        tk.Button(self.master, text="Add Port", command=self.add_serial_port).grid(row=0, column=2, padx=5, pady=5)

    def add_serial_port(self):
        # Add a new serial window for the selected port
        device = self.port_dropdown.cget("text")
        if device not in self.selected_devices:
            self.selected_devices.append(device)
            SerialWindow(device)

if __name__ == "__main__":
    root = tk.Tk()
    app = SerialReaderGUI(root)
    root.mainloop()

```

In this implementation, the `SerialWindow` class uses the `start_reading` function to start a new thread that reads from the serial port using the `read_serial_port` function. The `read_serial_port` function updates the text area with each line of data received from the serial port. The `SerialReaderGUI` class calls the `start_reading` function after the window is created, so the serial port is read in a separate thread without blocking the main GUI loop.


***

Exported on March 18, 2023 12:16 AM.