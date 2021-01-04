# Simulate an AXI4-Lite Peripheral using VIvado Simulator

When designing an AXI4 IPcore we want to verify the circuit.

Two ways to do this is 
* Simulating the circuit before implementation
* Probing the signals with a logic analyzer post generation (internal or external to the FPGA)

  * The ILA (Integrated Logic Analyzer) is a tool for in hardware debugging.
It needs to be generated in fabric as a memory sampling certain signals adding complexity to the design.

  * Becuase of this, it’s best practice to write a testbench to simulate IP cores before implementation.
  
Simulation of an AXI4 IPcore requires emulating the signals on the AXI bus for write and read transactions.

#### Step 1: Create an AXI4 IP


| Peripheral interface:| |
| ------------ | ------------- |
| Type:| Lite |
| Mode:| Slave |
| Data width (Bits):| 32 |
| Number of registers:| 4 |

[Image 1. Create AXI4 Peripheral](https://raw.githubusercontent.com/TsafasN/AXI4_lite-Simulation-Tutorial/gh-pages/Create_Peripheral2.PNG)

#### Step 2: Understand the AXI4 transaction handshake mechanism

For simulating the AXI bus, your tasks will need to drive the address, data, and response lines relevant to the transaction. The task will also need to respond to the handhsaking signals from the AXI4-lite slave (in this case the LED IPcore).

First step in writing a AXI4 testbench is to define all the signals used by the AXI4-lite interface. Since our Task will be controlling the Master signals, those should be set as reg type. The slave signals will be driven by our IPcore and should be wire's. Next, instantiate your IP core, making the appropriate port connections to the previously defined AXI4-lite signals.


| **Interface channels:** | |
| :---: | :---: |
| Read Address channel | (AR) |
| Read Data channel | (R) |
| Write Address channel | (AW) |
| Write Data channel | (W) |
| Write Response channel | (B) |

All five transaction channels use the same VALID/READY handshake process to transfer address, data, and control information.

Handshake occurs as described in the steps below(in any channel)

1. The source generates the VALID signal to indicate when the address, data or control information is available.
2. The destination generates the READY signal to indicate that it can accept the information.
3. Transfer occurs only when both the VALID and READY signals are HIGH.

##### Write transfer eg.
```
A master places an address on the AWADDR line and asserts a valid signal. 
The slave asserts that it's ready to receive the address and the address is transferred.

The master places data on the bus and asserts the valid signal (WVALID). 
When the slave is ready, it asserts WREADY and data transfer begins.   
```

[Image 1. Create AXI4 Peripheral](https://raw.githubusercontent.com/TsafasN/AXI4_lite-Simulation-Tutorial/gh-pages/Create_Peripheral2.PNG)
[Image 1. Create AXI4 Peripheral](https://raw.githubusercontent.com/TsafasN/AXI4_lite-Simulation-Tutorial/gh-pages/Create_Peripheral2.PNG)
[Image 1. Create AXI4 Peripheral](https://raw.githubusercontent.com/TsafasN/AXI4_lite-Simulation-Tutorial/gh-pages/Create_Peripheral2.PNG)




#### Step 3: Create a transaction mechanism

#### Step 4: Implement the testbench in VHDL

#### Step 5: Simulate the IP





You can use the [editor on GitHub](https://github.com/TsafasN/AXI4_lite-Simulation-Tutorial/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/TsafasN/AXI4_lite-Simulation-Tutorial/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
