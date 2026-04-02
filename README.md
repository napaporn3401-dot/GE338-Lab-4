# Flood Risk Modeling using Multi-Criteria Analysis (MCA) in Google Earth Engine

## Overview
This project develops a spatial flood risk model for Tak Province, Thailand using Multi-Criteria Analysis (MCA) implemented in Google Earth Engine (GEE).

The model integrates multiple environmental factors to generate a flood susceptibility map.

---

## Research Question
Which areas in Tak Province are most vulnerable to flooding based on physical and environmental factors?

---

## Methodology

### 1. Data Sources
- DEM: USGS SRTM
- Rainfall: ERA5 Daily Aggregated
- Land Cover: MODIS MCD12Q1
- Rivers: WWF HydroSHEDS

---

### 2. Data Preprocessing
All input layers were clipped to the study area (Tak Province) and prepared in raster format.

---

### 3. Normalization
Each factor was normalized using Min-Max scaling:

\[
X' = \frac{X - X_{min}}{X_{max} - X_{min}}
\]

This ensures all variables are on a comparable scale (0–1).

---

### 4. Weighted Overlay Model

Flood risk was calculated using the weighted linear combination:

\[
FloodRisk = (0.30 \cdot Rain) + (0.25 \cdot Slope) + (0.20 \cdot Elevation) + (0.15 \cdot River) + (0.10 \cdot Landcover)
\]

---

### 5. Classification
Flood risk values were classified into three categories:

- Low Risk: < 0.25
- Medium Risk: 0.25 – 0.45
- High Risk: > 0.45

---

## Sensitivity Analysis
A sensitivity analysis was conducted by varying the weight of rainfall by ±20%.

The results indicate that the model is highly sensitive to rainfall and slope, confirming their dominant influence on flood risk.

---

## Validation
Due to the lack of ground truth data, validation was performed qualitatively by comparing model outputs with known flood-prone regions and satellite-based datasets.

---

## Results
The model successfully identifies flood-prone areas, particularly low-lying regions near rivers and areas with low slope.

---

## Limitations
- Lack of ground truth data for quantitative validation
- Simplified weighting scheme
- Static model without temporal variation
- Differences in spatial resolution among datasets

---

## Conclusion
The MCA approach provides a useful framework for flood risk assessment. However, the accuracy of the model depends heavily on the quality of input data and the weighting scheme.

---
## Sensitivity Analysis

The model was tested by adjusting the weight of the rainfall factor by ±20%.

Two scenarios were evaluated:
- Increased rainfall weight (0.30 → 0.36)
- Decreased rainfall weight (0.30 → 0.24)

### Observations:
- Areas near rivers showed consistent high risk across scenarios.
- Low-lying regions remained sensitive to weight changes.
- Some boundary areas changed classification, indicating model uncertainty.

### Conclusion:
The model is most sensitive to rainfall and slope, suggesting these are the dominant drivers of flood risk in the study area.
## Repository Structure
GE338-Lab-4/
├── lab4_modeling.ipynb  
├── conceptual_framework.md  
├── README.md  
├── figures/  
ภารกิจที่ 1: Conceptual Framework
คำถามวิจัย
พื้นที่ใดในจังหวัดตากที่มีความเสี่ยงต่อการเกิดน้ำท่วมสูง เมื่อพิจารณาจากปัจจัยทางภูมิศาสตร์และสิ่งแวดล้อม เช่น ปริมาณฝน ความสูงของพื้นที่ ความลาดชัน ระยะห่างจากแม่น้ำ และการใช้ประโยชน์ที่ดิน
คำถามนี้สามารถตอบได้ในรูปแบบของ “แผนที่ความเสี่ยงน้ำท่วม (Flood Risk Map)” ซึ่งแสดงการกระจายเชิงพื้นที่ของระดับความเสี่ยง

ปัจจัยที่ใช้และหลักการทางวิทยาศาสตร์
1.	ปริมาณฝน (Rainfall)
เป็นตัวกระตุ้นหลักของการเกิดน้ำท่วม ปริมาณฝนที่สูงจะเพิ่ม runoff และอาจทำให้ระบบระบายน้ำไม่สามารถรองรับได้ 
2.	ความลาดชัน (Slope)
ความลาดชันมีผลต่อความเร็วในการไหลของน้ำ พื้นที่ที่มี slope ต่ำจะทำให้น้ำไหลช้าลงและมีแนวโน้มสะสมตัวมากกว่า 
3.	ความสูงของพื้นที่ (Elevation)
พื้นที่ที่มีระดับความสูงต่ำมักเป็นพื้นที่รับน้ำ (floodplain) จึงมีความเสี่ยงสูงกว่าพื้นที่สูง 
4.	ระยะห่างจากแม่น้ำ (Distance to River)
พื้นที่ที่อยู่ใกล้แม่น้ำมีความเสี่ยงจากการเอ่อล้นของแม่น้ำ (river overflow) 
5.	การใช้ประโยชน์ที่ดิน (Land Cover)
พื้นที่เมืองหรือสิ่งปลูกสร้างมีพื้นผิวไม่ซึมน้ำ (impervious surface) ทำให้ runoff สูง ในขณะที่พื้นที่ป่าช่วยเพิ่มการซึมน้ำและลดความเสี่ยง 

การกำหนดน้ำหนัก (Weight)
น้ำหนักของแต่ละปัจจัยกำหนดโดยอาศัย Expert Knowledge และหลักการทางอุทกวิทยา (Hydrological reasoning) โดยพิจารณาความสำคัญสัมพัทธ์ของแต่ละปัจจัยต่อการเกิดน้ำท่วม
•	Rainfall = 0.30 (มีผลโดยตรงมากที่สุด) 
•	Slope = 0.25 
•	Elevation = 0.20 
•	Distance to River = 0.15 
•	Land Cover = 0.10 
น้ำหนักรวมเท่ากับ 1 และสะท้อนลำดับความสำคัญของปัจจัยเชิงกายภาพที่มีผลต่อการเกิดน้ำท่วม

การตรวจสอบโมเดล (Validation)
โมเดลสามารถตรวจสอบได้โดยเปรียบเทียบกับข้อมูลจริง เช่น:
•	MODIS Flood products 
•	JRC Global Surface Water 
•	ข้อมูลเหตุการณ์น้ำท่วมย้อนหลัง 
การเปรียบเทียบสามารถทำได้ทั้งเชิงพื้นที่ (spatial overlap) และเชิงสถิติ (accuracy, confusion matrix) หากมีข้อมูล ground truth

ภารกิจที่ 2: Spatial Model (MCA)
การ Normalize
ใช้วิธี Min-Max Normalization
เหตุผล:
•	ทำให้ค่าของทุกปัจจัยอยู่ในช่วง 0–1 
•	ลดปัญหาความต่างของหน่วย 
•	ทำให้สามารถนำมารวมกันได้อย่างเหมาะสม 

การรวมปัจจัย (Weighted Linear Combination)
Flood risk
เหตุผล:
•	เป็นวิธีมาตรฐานใน Multi-Criteria Analysis (MCA) 
•	สามารถตีความได้ง่าย 
•	แสดงอิทธิพลเชิงสัดส่วนของแต่ละปัจจัย 

การแบ่งระดับความเสี่ยง (Thresholds)
กำหนดช่วงความเสี่ยงเป็น 3 ระดับ:
•	Low Risk: < 0.25 
•	Medium Risk: 0.25 – 0.45 
•	High Risk: > 0.45 
เหตุผล:
•	ใช้การแบ่งแบบ threshold ตามการกระจายของค่าผลลัพธ์ 
•	หรืออิง expert judgment เพื่อแบ่งระดับที่เหมาะสมสำหรับการตีความเชิงนโยบาย 

การตีความผลลัพธ์
แผนที่ผลลัพธ์สามารถใช้เพื่อ:
•	ระบุพื้นที่เสี่ยงน้ำท่วม 
•	สนับสนุนการวางแผนเชิงพื้นที่ 
•	ใช้ในการจัดการความเสี่ยงและการเตรียมรับมือภัยพิบัติ 
ภารกิจที่ 3: Sensitivity Analysis
การวิเคราะห์ความไวของโมเดลทำโดยการปรับค่าน้ำหนักของปัจจัยหลัก (เช่น rainfall) เพิ่มขึ้นและลดลงประมาณ ±20%
ตัวอย่าง:
•	Rainfall = 0.30 → 0.36 (+20%) 
•	Rainfall = 0.30 → 0.24 (-20%) 
จากการทดลองพบว่า:
•	พื้นที่ใกล้แม่น้ำและพื้นที่ลุ่มยังคงมีความเสี่ยงสูงอย่างสม่ำเสมอ (robust areas) 
•	บางพื้นที่มีการเปลี่ยนแปลงระดับความเสี่ยงเมื่อปรับน้ำหนัก (sensitive areas) 
สรุปได้ว่าโมเดลมีความไวต่อปัจจัย rainfall และ slope ซึ่งเป็นปัจจัยหลักในการกำหนดการเกิดน้ำท่วม
ผลการวิเคราะห์นี้ช่วยเพิ่มความเข้าใจเกี่ยวกับความไม่แน่นอนของโมเดล และแสดงให้เห็นว่าโมเดลมีความน่าเชื่อถือในพื้นที่ที่ผลลัพธ์ไม่เปลี่ยนแปลงมากเมื่อปรับน้ำหนัก
ภารกิจที่ 4: Validation กับข้อมูลจริง
การตรวจสอบความถูกต้องของโมเดลสามารถทำได้โดยเปรียบเทียบกับข้อมูลน้ำท่วมจริง เช่น:
•	MODIS Flood datasets 
•	JRC Global Surface Water 
•	ข้อมูลพื้นที่น้ำท่วมจากหน่วยงานรัฐ 
อย่างไรก็ตาม หากไม่มีข้อมูล ground truth:
•	การ validation เชิงปริมาณอาจทำได้ยาก 
•	สามารถใช้การ validation เชิงคุณภาพ (visual comparison) แทน 
ในทางปฏิบัติ สามารถ validate ได้โดย:
•	ซ้อนทับแผนที่ flood risk กับข้อมูล flood จริง 
•	ตรวจสอบว่าพื้นที่เสี่ยงสูงตรงกับพื้นที่ที่เคยเกิดน้ำท่วมหรือไม่ 

คำถามสำหรับ README
1. ถ้ามี Ground Truth จริง คิดว่า Accuracy จะอยู่ระดับใด? เพราะอะไร?
คาดว่า accuracy จะอยู่ในระดับปานกลางถึงค่อนข้างดี เนื่องจากโมเดลใช้ปัจจัยหลักที่มีผลต่อการเกิดน้ำท่วมจริง เช่น ปริมาณฝน ความลาดชัน และความสูงของพื้นที่ อย่างไรก็ตามความแม่นยำอาจลดลงเนื่องจากข้อจำกัดของน้ำหนักที่กำหนดแบบ expert judgment และการไม่รวมปัจจัยเชิงพลวัต เช่น การระบายน้ำและโครงสร้างพื้นฐาน

2. ปัจจัยที่ไม่ได้ใส่ในโมเดลแต่สำคัญ
•	ความสามารถในการระบายน้ำ (drainage system) 
•	โครงสร้างพื้นฐาน (เขื่อน คลอง) 
•	ความหนาแน่นของประชากร 
•	ลักษณะดิน (soil type) 
•	การเปลี่ยนแปลงการใช้ที่ดินตามเวลา 
เหตุผลที่ไม่รวม:
•	ข้อจำกัดด้านข้อมูล (data availability) 
•	ความซับซ้อนของโมเดล 
•	ข้อจำกัดด้านเวลาและทรัพยากร 

3. โมเดลนี้เหมาะกับ Scale ใด?
โมเดลเหมาะกับระดับ จังหวัดหรือระดับภูมิภาค (regional scale) เนื่องจาก:
•	ใช้ข้อมูลความละเอียดปานกลางถึงหยาบ 
•	เหมาะสำหรับการวิเคราะห์เชิงนโยบาย 
•	ไม่เหมาะกับการใช้งานระดับแปลงหรือพื้นที่ขนาดเล็กมาก 

4. การอัปเดตโมเดลรายปี
สิ่งที่ต้องทำซ้ำ:
•	การดึงข้อมูล rainfall ใหม่ 
•	การอัปเดต land cover 
•	การคำนวณ normalization ใหม่ 
•	การรัน model ใหม่ 
สิ่งที่คงที่:
•	โครงสร้างของโมเดล 
•	วิธีการคำนวณ 
•	น้ำหนัก (หากไม่เปลี่ยน methodology)
