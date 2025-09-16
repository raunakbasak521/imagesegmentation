
# 🔬 Image Segmentation for Electrode Wetting Analysis  

## 📖 Project Overview  
This project uses **image segmentation** to analyze how well the **electrolyte wets the surface of battery electrodes** (cathode and anode).  

When a battery is made, the electrolyte should spread evenly across the electrode surface. If some areas remain **dry**, those regions don’t contribute to the battery’s performance. This reduces:  
- ⚡ **Voltage (EMF)**  
- 🔋 **Capacity**  
- ⚙️ **Efficiency**  

By applying Meta AI’s **Segment Anything Model (SAM)**, this project identifies **wet vs. dry regions** of the electrode and calculates the **wetting fraction**.  

---

## 👥 Common Man’s Explanation  
Think of a battery like a sponge that needs to be fully soaked in liquid to work properly. If parts of the sponge stay dry, they don’t hold or release energy.  

This project is like giving the computer special glasses 🥽 to look at the electrode surface and figure out:  
- ✅ which parts got wet  
- ❌ which parts stayed dry  

The more wet area, the better the battery will perform.  

---

## 🧑‍💻 Technical Explanation  
The code leverages **Meta’s Segment Anything Model (SAM)** for region-based segmentation of electrode surface images.  

### Workflow:  
1. Load electrode surface image.  
2. Provide bounding box coordinates for total electrode and subregions.  
3. Run SAM to generate segmentation masks.  
4. Compute:  
   - **Total electrode area** (in square pixels).  
   - **Dry area** = (sum of all segmented regions) − (max electrode area).  
   - **Wetting fraction** = `1 − (dry_area / mask_area)`.  

This provides a quantitative measure of **electrolyte wetting uniformity**.  

---

## ⚙️ Requirements  
- Python 3.8+  
- [PyTorch](https://pytorch.org/)  
- OpenCV  
- Matplotlib  
- NumPy  
- [Segment Anything](https://github.com/facebookresearch/segment-anything)  

Install dependencies:  
```bash
pip install numpy torch matplotlib opencv-python
pip install git+https://github.com/facebookresearch/segment-anything.git
```

---

## 🚀 Usage  

### 1. Clone the repository and navigate to project folder  
```bash
git clone https://github.com/USERNAME/electrode-wetting-segmentation.git
cd electrode-wetting-segmentation
```

### 2. Place your input images  
- Electrode image → `input/new_imageform.bmp`  
- Coordinate template → `input/coordinate_example.JPG`  
- Model checkpoint → `/content/drive/MyDrive/Image Analysis/sam_vit_b_01ec64.pth`  

### 3. Run the script  
```bash
python segmentation.py
```

### 4. Enter coordinates when prompted  
Coordinates must be entered as **x1 y1 x2 y2 ...** (top-left and bottom-right corners of bounding boxes).  

### 5. Output  
- Visualizations of segmented regions.  
- Terminal prints:  
  - **Total electrode area (pixels)**  
  - **Dry area (pixels)**  
  - **Wetting fraction**  

---

## 📊 Example Output  
```bash
The total electrode area (in sq pixels) =  523450
Total dry area =  78120
Wetting Fraction =  0.85
```

This means **85% of the electrode surface was wetted by the electrolyte**, and 15% remained dry.  

---

## 🧠 Context & Applications  
- **Battery R&D**: Helps optimize electrolyte filling processes.  
- **Quality Control**: Detects defects in electrode manufacturing.  
- **Performance Analysis**: Links wetting fraction to capacity fade and efficiency loss.  

---

## 📂 Repository Structure  
```
├── segmentation.py          # Main code
├── input/                   # Input images
│   ├── new_imageform.bmp
│   └── coordinate_example.JPG
├── output/                  # Segmentation results
└── README.md                # Documentation
```

---

## 🙌 Acknowledgements  
- [Meta AI’s Segment Anything Model](https://github.com/facebookresearch/segment-anything)  
- OpenCV, NumPy, Matplotlib  
