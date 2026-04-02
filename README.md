ส่วนที่ 1: Problem Statement 

Specific — ระบุพื้นที่และประชากร/ระบบนิเวศที่ได้รับผลกระทบได้ชัดเจน 

     พื้นที่จังหวัดกรุงเทพมหานคร นนทบุรี ปทุมธานี 

Measurable — มีตัวชี้วัดที่สามารถวัดได้ด้วย Remote Sensing หรือ GIS 

 

Land Surface Temperature (LST): MODIS 

NDVI (ความหนาแน่นพืช): Sentinel-2 

Soil Moisture / Rainfall (CHIRPS): NASA_USDA_HSL (SMAP10KM) 

Urban built-up: Landsat classification 

 

Relevant — เชื่อมโยงกับปัญหาจริงในบริบทไทยหรือภูมิภาค 

ไทยเป็นเขตร้อนชื้น 

พื้นที่เมือง มี heat island และน้ำขัง เชื้อราเติมโตง่าย  

เชื้อราในดิน/พืช 

เกี่ยวกับโรคทางเดินหายใจ 

 

Researchable ใน 4 สัปดาห์ — ไม่ใหญ่เกินไปจนทำไม่ได้จริง 

MODIS (LST) 

Sentinel-2 (NDVI) 

CHIRPS (rainfall) 

 

 

 

 

Researcher Question 

พื้นที่ใดในกรุงเทพมหานคร นนทบุรี และปทุมธานีมีความเหมาะสมต่อการเจริญของเชื้อราสูงที่สุด 

Data set  

Sentinel 2 ใช้ดู NDVI Band : B8 (NIR), B4 (RED) 

SMAP Soil moisture variable : soil moisture  

ERA5 Temperature variable: temperature_2m 

Landsat Urban Classification variable : urban class 

วิธีการวิเคราะห์ 

คำนวณ NDVI จาก Sentinel-2 

Normalize ทุกตัวแปรให้อยู่ในช่วง 0–1 

รวมตัวแปรด้วย Weighted Overlay 

Soil moisture (0.4) 

NDVI (0.3) 

Temperature (0.2) 

Urban (0.1) 

สร้าง Fungal Suitability Index 

ความละเอียด ใช้ resolution ประมาณ 500 m – 1 km 

 

NDVI มีความสัมพันธ์กับการกระจายของความเสี่ยงเชื้อราอย่างไรในเชิงพื้นที่? 

Data set  

Sentinel-2 NDVI Band: B8, B4 

Fungal Risk Map (จาก RQ1) 

วิธีการวิเคราะห์ 

แบ่งค่า NDVI เป็นระดับ (ต่ำ / กลาง / สูง) 

Overlay กับ Fungal Risk Map 

ใช้ 

Correlation analysis 

Zonal statistics 

วิเคราะห์ 

NDVI สูง → risk สูงหรือไม่ 

ความละเอียด 

ใช้ resolution 10–30 m (Sentinel-2)หรือ upscale เป็น ~500 m เพื่อให้เท่ากับตัวแปรอื่น 

พื้นที่ใดในกรุงเทพมหานคร นนทบุรี และปทุมธานีมีความเหมาะสมต่อการเจริญของเชื้อราสูงที่สุด 

Data set  

Sentinel 2 ใช้ดู NDVI Band : B8 (NIR), B4 (RED) 

SMAP Soil moisture variable : soil moisture  

ERA5 Temperature variable: temperature_2m 

Landsat Urban Classification variable : urban class 

วิธีการวิเคราะห์ 

คำนวณ NDVI จาก Sentinel-2 

Normalize ทุกตัวแปรให้อยู่ในช่วง 0–1 

รวมตัวแปรด้วย Weighted Overlay 

Soil moisture (0.4) 

NDVI (0.3) 

Temperature (0.2) 

Urban (0.1) 

สร้าง Fungal Suitability Index 

ความละเอียด ใช้ resolution ประมาณ 500 m – 1 km 

 

Data Inventory 

Dataset 

Source/Collection 

ใช้ตอบคำถามข้อ 

ข้อจำกัดที่รู้แล้ว 

Sentinel-2 MSI 

COPERNICUS/S2 

RQ1, RQ2 

ปัญหาเมฆปกคลุม (Cloud cover) ในพื้นที่กรุงเทพฯ นนทบุรี และปทุมธานี 

SMAP 

(NASA-USDA) 

NASA_USDA_HSL/ 

SMAP10KM 

RQ1, RQ2 

ความละเอียดเชิงพื้นที่ต่ำ (10km) อาจต้องมีการจัดรูปแบบข้อมูล 

ให้เข้ากับตัวแปรอื่น 

ERA5-Land 

ECMWF/ERA5_LAND/ 

MONTHLY_BY_HOUR 

RQ1 

ข้อมูลเป็นค่าเฉลี่ยรายชั่วโมง/เดือน อาจไม่สะท้อน Micro-climate ในบางจุด 

Landsat 8/9 

LANDSAT/LC08/ 

C02/T1_L2 

RQ2 

รอบการบันทึกภาพ (Temporal resolution) ห่างกันประมาณ 16 วัน 

 

ส่วนที่ 4: Methodology Flow 

 ขั้นตอนการทำงาน 

1. Data Collection 

•	โหลดข้อมูลจาก Google Earth Engine 

•	ตัดเฉพาะพื้นที่กรุงเทพมหานคร นนทบุรี ปทุมธานี 

2. Preprocessing 

•	กำจัดเมฆ (Cloud masking) 

•	คำนวณ NDVI 

•	ปรับค่าข้อมูลให้อยู่ในช่วง 0–1 (Normalization) 

3. Feature Preparation 

รวมตัวแปร: 

•	NDVI 

•	LST (Land Surface Temperature) 

•	Urban density 

•	Soil moisture 

4. การวิเคราะห์ 

วิธีที่ 1: Weighted Overlay 

•	กำหนดน้ำหนัก เช่น 

•	Urban = 0.4 

•	Temperature = 0.3 

•	NDVI = 0.2 

•	Soil moisture = 0.1 

•	สร้าง Risk Index 

วิธีที่ 2: Machine Learning 

•	ใช้ Random Forest 

•	แบ่ง train/test 

•	ทำนายพื้นที่เสี่ยง 

5. Validation 

•	Accuracy จาก train/test 

•	เปรียบเทียบกับพื้นที่เมืองหนาแน่น 

6. Output 

•	แผนที่ความเสี่ยง (สูง / กลาง / ต่ำ) 

•	Visualization บน GEE 

Feasibility และ Risk Assessment 

1.ความเสี่ยงหลักของโครงการ 

Data Availability (Cloud Cover): พื้นที่กรุงเทพฯ นนทบุรี และปทุมธานี มีโอกาสเจอเมฆปกคลุมสูง โดยเฉพาะหากเลือกช่วงเวลาที่เป็นฤดูฝน ทำให้ค่า NDVI จาก Sentinel-2 คลาดเคลื่อน 

Ground Truth Gap: ข้อมูลที่วิเคราะห์เป็นเพียง "ความเหมาะสม (Suitability)" แต่ยังขาดข้อมูลการระบาดจริงของเชื้อราในระดับพื้นที่เพื่อนำมา Validate ผลลัพธ์ 

2.Plan B ถ้าเจอปัญหาแต่ละอย่าง

กรณีเมฆเยอะ: ใช้การทำ Median/Mean Composite จากภาพถ่ายหลายช่วงเวลา หรือเปลี่ยนไปใช้ข้อมูลจากดาวเทียมดวงอื่นที่ในช่วงเวลาใกล้เคียงกัน

กรณี Parameter ไม่ชัดเจน: ปรับสัดส่วนน้ำหนัก (Weight) ในการทำ Weighted Overlay โดยอิงจากงานวิจัย (Paper) ที่เกี่ยวข้องกับปัจจัยการเติบโตของเชื้อราเป็นหลัก

3.ขอบเขตที่จะ Descope ออกถ้าเวลาไม่พอ

ลดจำนวนจังหวัดในการศึกษา เหลือเพียงกรุงเทพมหานครเพียงจังหวัดเดียว
