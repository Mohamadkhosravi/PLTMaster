
---

# **System Initialization and Configuration Documentation**

## **1. General System Overview**

The system comprises three key components interacting with each other:
- **GUI** (Graphical User Interface)
- **Main Controller**
- **Sensors**

These modules communicate bidirectionally:
```
GUI <--> MAIN <--> SEN (Sensors)
```

---

## **2. Initialization Phases**

### **2.1 System Initialization Steps**
1. **Init**
2. **Connect / Manage Comm**
3. **Event Manager**

---

## **3. Voltage Regulator Initialization**

### **3.1 Subsystems Initialization**
- **Voltage Regulator Init**
- **Voltage Selection Init**
- **Line Check and Current Monitor Init**
- **PLT TX Init**
- **PLT RX Init**

---

### **3.2 Voltage Regulator Init**
#### **Steps**
1. **Set VR** (Variable Resistors) to **MIN**
2. **Enable Regulator**
3. **Get & Read ADC Regulator Vout**
4. **Set VR to MAX**
5. **Get & Read ADC**
5. **Set VR (UP / DOWN) To Defult Value**
6. **Get & Read Reglator Voltage Regulator **

#### **Error Conditions**
1. In Step 2:  
   - If **Enable Regulator** Return Error , handled **Enable Error** .
2. In Step 3:  
   - If **Vout < Vout_MIN**, take corrective action.
3. In Step 5:  
   - If **Vout > Vout_MAX**, handle the condition.
4. In Step 6:
  - If **If **Vout ≠ V Default**, take corrective action .


#### **Error Handling**
- Errors are processed and handled appropriately during initialization steps.

---
![Flowchart](./Flowcharts/Voltage%20Regulator%20Init.drawio.png)

## **3.3 Voltage Selection Init**

### **Steps:**
1. **Disable Voltage Regulator Up and Down**  
2. **Enable Voltage Regulator Up / Down**  
3. **Enable Voltage Selection**
4. **Select Voltage Regulator Up/Down**  
5. **Get Read Voltage Line**
- **Repeat This steps once for both **Up** and **Down****

6. **Enable Voltage Regulator Up and Down**
7. **Select Between Voltage Regulator Up and after that Down AND Get Read Voltage Line**

### **Error Conditions:**
1.  In Step 2:
      - **Enable Error** if the voltage regulator cannot be enabled properly.
2. In Step 3: 
    - If in the elected Up/Down  **s voltage line ≠ Voltage Reg Up Or Down ±0.5V**, take corrective action.

2. In Step 7:
      - if the **Time of swing** between voltage Up and Down < 0.2/BITRATE  , it will trigger an error.


---
#### **Error Handling**
- Errors are processed and handled appropriately during initialization steps.

---
## **3.4 Line Check and Current Monitor Init **