# data/polar (ทางเลือก — ส่วนเสริม Doppler ของ Notebook 3)

ไฟล์ polar ขนาดเล็ก (CfRadial, int16) ของเรดาร์ KKN เวลา **09:15, 09:30, 09:45 UTC** วันที่ 3 พ.ค. 2567
มีตัวแปร `reflectivity_qc`, `velocity_qc` (ยังไม่แก้ aliasing; Nyquist 8.38 m/s), `spectrum_width_qc`, ZDR, ΦDP, ρHV และ `qc_flag`

**วิธีสร้าง (ผู้สอน):** รัน `00_prepare_polar_for_doppler_pytda_hid.ipynb` (repo ที่สอง) โดยตั้ง
`REPO2_TIMES = ["20240503_0915", "20240503_0930", "20240503_0945"]`
แล้วคัดลอกไฟล์ `KKN_20240503_HHMM_polar.nc` ทั้ง 3 ไฟล์มาไว้ในโฟลเดอร์นี้ (ไฟล์ละ ~0.5–2 MB)

ถ้าไม่มีไฟล์ Notebook 3 จะข้ามส่วนนี้ให้อัตโนมัติ
