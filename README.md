# Nowcasting พายุฤดูร้อนภาคอีสานด้วยเรดาร์ขอนแก่น (KKN) และ pysteps

ชุด notebook สำหรับสอน **radar nowcasting และการวิเคราะห์พายุฤดูร้อน** ด้วย [pysteps](https://pysteps.readthedocs.io/en/stable/) โดยใช้ **ข้อมูลจริงจากเรดาร์ขอนแก่น (KKN) กรมอุตุนิยมวิทยา**
กรณีศึกษา **พายุฤดูร้อน 3 พฤษภาคม 2567** ที่ทำให้บ้านเรือนเสียหายมากกว่า 1,000 หลัง ผู้เสียชีวิต 4 ราย ใน 5 จังหวัด

| เวลา (น.) | พื้นที่ | เหตุการณ์ |
|---|---|---|
| 14:00 | อ.ภูกระดึง จ.เลย | ลมกระโชกแรง ลูกเห็บ บ้านเสียหาย 27 หลัง |
| 16:30 | 4 อำเภอ จ.หนองบัวลำภู (นากลาง, สุวรรณคูหา หนักสุด) | ลมกระโชกแรง ลูกเห็บ บ้านเสียหาย > 750 หลัง "หนักที่สุดในรอบ 50 ปี" |
| ~17:00 | อ.ศรีเชียงใหม่ สังคม เมือง จ.หนองคาย | ลมแรง บ้านเสียหาย ~176 หลัง |
| กลางคืน | อ.เมือง จ.บึงกาฬ | สะพานลอยหลุด รถเครนล้ม ผู้เสียชีวิต 3 ราย |
| กลางคืน | อ.เมือง จ.ขอนแก่น | ลมกระโชก ลูกเห็บ ผู้เสียชีวิต 1 ราย |

เหมาะสำหรับนิสิตปริญญาตรีปี 3–4 และปริญญาโท สาขาวิทยาศาสตร์สิ่งแวดล้อม/ภูมิศาสตร์ คำอธิบายทั้งหมดเป็น **ภาษาไทย** (ศัพท์เทคนิคใช้ทับศัพท์) ส่วนข้อความในรูปเป็นภาษาอังกฤษ เพื่อนำไปใช้ในบทความวิชาการได้ทันที
ต่อยอดจาก repo [Teach_Nowcast_Pysteps_TMD](https://github.com/nattaponm/Teach_Nowcast_Pysteps_TMD) (พายุลูกเห็บเชียงของ เรดาร์เชียงราย)

## 📚 ลำดับการเรียน

| # | Notebook | เนื้อหา | เครื่องมือหลัก | เวลา |
|---|---|---|---|---|
| 0 | [`00_prepare_pcappi_for_pysteps`](notebooks/00_prepare_pcappi_for_pysteps.ipynb) | **(ผู้สอน)** อ่าน UF ดิบ → QC → pseudo-CAPPI 2 km → NetCDF ใน `data/` (ต้องมีไฟล์ดิบใน Drive) | Py-ART | – |
| 1 | [`01_summer_storm_environment_radar`](notebooks/01_summer_storm_environment_radar.ipynb) | **Skew-T, CAPE/CIN/DCAPE**, วงจรชีวิตพายุทั้งวัน, แผนที่ความเสียหาย, เรดาร์เทียบเวลารายงาน | MetPy, `kt.point_series` | 75–90 นาที |
| 2 | [`02_storm_intensity_hail`](notebooks/02_storm_intensity_hail.ipynb) | **Z–R 3 แบบ + hail cap**, ฝนสะสม, **convective/stratiform (Steiner)**, แกนพายุและสัญญาณลูกเห็บ, ลำคลื่น 4 มุมยกเทียบระดับเยือกแข็ง, dBR | `dB_transform` | 75 นาที |
| 3 | [`03_motion_extrapolation_interpolation`](notebooks/03_motion_extrapolation_interpolation.ipynb) | LK/VET/DARTS, **advection vs propagation** (เทียบลมจาก sounding), **Hovmöller**, extrapolation, interpolation 15 → 5 นาที, (เสริม) **Doppler & spectrum width** | `motion`, `extrapolate` | 75–90 นาที |
| 4 | [`04_deterministic_nowcast`](notebooks/04_deterministic_nowcast.ipynb) | Persistence vs Extrapolation vs **S-PROG** vs **ANVIL**, verification ตามช่วงชีวิตพายุ (CSI, FSS), **เวลาเตือนล่วงหน้าที่นากลาง**, GeoTIFF | `sprog`, `anvil`, `verification` | 75–90 นาที |
| 5 | [`05_probabilistic_nowcast`](notebooks/05_probabilistic_nowcast.ipynb) | **STEPS ensemble**, ความน่าจะเป็น pixel vs neighbourhood ณ จุดเกิดเหตุ, ROC/reliability/rank histogram, **กรณีพลาด (ภูกระดึง)**, **cost–loss** | `steps`, `probscores` | 90 นาที |
| 6 | [`06_storm_tracking_tdating`](notebooks/06_storm_tracking_tdating.ipynb) | **T-DaTing** ปรับพารามิเตอร์สำหรับ KKN, เส้นทางพายุบนภูมิประเทศ, จุดกำเนิดเทียบความสูง, วงจรรายวัน, **เซลล์ใดถล่มที่ไหน/กี่โมง**, GeoPackage | `feature.tstorm`, `tracking.tdating` | 90 นาที |

ทุก notebook มีโครงสร้างเดียวกัน
🎯 วัตถุประสงค์ → 📖 แนวคิดและสมการ → ⚙️ setup → 💻 ลงมือทำ → 🧪 แบบฝึกหัด (💡 คำใบ้ + ✅ เฉลยในเซลล์ที่ซ่อนโค้ดไว้) → 📝 สรุปและคำถามชวนคิด → 📚 อ้างอิง

## 🚀 วิธีใช้ (นิสิต)
1. เปิดใน Colab: `https://colab.research.google.com/github/nattaponm/Teach_Pysteps_KKN_summerStorm/blob/main/notebooks/<ชื่อไฟล์>.ipynb` (หรือกดปุ่ม *Open in Colab* ด้านบนของแต่ละไฟล์)
2. **File → Save a copy in Drive**
3. รันเซลล์ **⚙️ Setup** ก่อน (ติดตั้ง pysteps แล้ว clone repo นี้ ประมาณ 2–3 นาที)
4. เริ่มจาก **Notebook 1** — ข้อมูลใน `data/` เตรียมไว้แล้ว ไม่ต้องรัน Notebook 0

รูปทุกรูปบันทึกเป็น **PNG 300 dpi + PDF** ในโฟลเดอร์ `figures/` ของ Colab session ส่วนผลลัพธ์ GIS (GeoTIFF, GeoPackage, CSV) อยู่ใน `output/`

## 📁 โครงสร้าง repo
```
data/
  KKN_20240503/
    KKN_20240503_pcappi2km_dbz.nc   pseudo-CAPPI 2 km, 1 km, ±240 km, ทุก 15 นาที ทั้งวัน (dBZ) → ทุก notebook
    manifest.json, *_inventory.csv, *_echo_stats.csv   ที่มาของข้อมูล/เวลาที่หายไป/พื้นที่ echo
  basemap/      ขอบเขตประเทศ–จังหวัด–อำเภอ (geoBoundaries) และภูมิประเทศสำหรับ hillshade
  reports/      KKN_20240503_reports.csv — รายงานความเสียหาย 19 จุด (ระดับตำบล) พร้อมแหล่งข่าว
  sounding/     ข้อมูลตรวจอากาศชั้นบนนครราชสีมา (48431) 1–3 พ.ค. 2567 00 UTC
  polar/        (ทางเลือก) ไฟล์ polar ขนาดเล็ก 09:15–09:45 UTC สำหรับส่วนเสริม Doppler ใน NB3
notebooks/      notebook 0–6
utils/
  data_io.py         อ่าน NetCDF → (Z, metadata) แบบ pysteps, บันทึก GeoTIFF, อ่านไฟล์ polar
  mapplot.py         แผนที่ระดับตีพิมพ์ (AEQD รอบเรดาร์, จังหวัด/อำเภอ, hillshade, วงระยะ 60 km, จุดรายงาน)
  kkn_tools.py       Z–R, convective/stratiform, ลำคลื่นเรดาร์, ความเร็ว/ทิศ, Hovmöller, interpolation, T-DaTing → GIS
  sounding_tools.py  Skew-T และดัชนี CAPE/CIN/DCAPE/shear ด้วย MetPy
figures/        รูปจาก Notebook 0 (การเตรียมข้อมูล)
```

## ⚙️ สมมติฐานและค่าที่ใช้ (ควรระบุในงานวิจัย)
| รายการ | ค่าที่ใช้ | หมายเหตุ |
|---|---|---|
| เวลา | **UTC** (เวลาไทย = UTC+7) | ไม่มีไฟล์ 04:00–04:45 UTC (11:00–11:45 น.) |
| เรดาร์ | KKN C-band, **4 มุมยก** (0.48°, 1.48°, 2.39°, 3.39°), gate 500 m, Nyquist 8.38 m/s | |
| ผลิตภัณฑ์ | **pseudo-CAPPI 2 km** เหนือเรดาร์ | ได้ค่าที่ 2 km จริงช่วง ~32–130 km; ไกลกว่านั้นข้อมูลมาจาก 2–5 km (`source_height_m`) |
| QC | ZH ≥ 0 dBZ, flare ray, non-met (ρHV < 0.70 และ ZH < 25 dBZ), speckle < 12 gates | gentle QC รักษาแกนพายุ (ดู NB0) |
| Z–R | Marshall–Palmer $Z = 200R^{1.6}$ + hail cap 55 dBZ | NB2 เปรียบเทียบกับ WSR-88D และ Rosenfeld tropical |
| T-DaTing | minref 33, maxref 45, mindiff 5, minsize 15, minmax 40, mindis 8, mintrack 2, match_frac 0.25 | ปรับสำหรับข้อมูล 15 นาที; ค่าตั้งต้นของ pysteps เจอเซลล์น้อยมาก (NB6 แบบฝึกหัด 6.1) |
| Sounding | นครราชสีมา 48431, 00 UTC (07:00 น.) | ห่างเรดาร์ ~190 km และก่อนพายุ 6–7 ชั่วโมง; ไม่มี 12 UTC |
| ตำแหน่งรายงาน | centroid ของตำบล | ความเสียหายจริงกระจายในตำบล จึงใช้ค่าในรัศมี 5–10 km |

## 🔎 สิ่งที่ข้อมูลเคสนี้แสดง (สรุปจาก notebook)
- **สภาพแวดล้อม:** CAPE ตอนบ่าย ~4,000 J/kg, **DCAPE ~1,450 J/kg** (เสี่ยง downburst), wind shear และลมอ่อนมาก
- **ก่อตัว** 12:00 น. บนที่สูง ~900 m ทางตะวันตก → **สูงสุด** 16:30–17:00 น. → **รวมตัว** เป็นระบบใหญ่ 17:00–20:30 น.
- กลุ่มพายุเคลื่อนไปทาง **ตะวันออก–ตะวันออกเฉียงเหนือ** และเร่งจาก ~10 เป็น ~50 km/h ขณะที่ลม 850–300 hPa เพียง ~11 km/h ไปทางตะวันออกเฉียงใต้ → **propagation** ครอบงำ
- แกนพายุ ≥ 45–50 dBZ ที่คงอยู่ 30–60 นาที ตรงกับ **นากลาง/สุวรรณคูหา**; nowcast เตือนล่วงหน้าได้เพียง ~15 นาที
- เรดาร์ช่วยประมาณเวลาเหตุ "กลางคืน": **บึงกาฬ ~20:45–21:00 น., อ.เมืองขอนแก่น ~19:15–22:00 น.**

## 📄 แหล่งข้อมูลและการอ้างอิง
- ข้อมูลเรดาร์: **กรมอุตุนิยมวิทยา (Thai Meteorological Department)** เรดาร์ขอนแก่น (KKN)
- ข้อมูลตรวจอากาศชั้นบน: University of Wyoming (สถานี 48431)
- ขอบเขตการปกครอง: [geoBoundaries](https://www.geoboundaries.org) (CC BY 4.0) | ตำแหน่ง centroid ตำบล: [OpenGISData-Thailand](https://github.com/chingchai/OpenGISData-Thailand)
- ภูมิประเทศ: AWS Open Data Terrain Tiles (SRTM/GMTED2010/ETOPO1)
- รายงานความเสียหาย: ปภ.จ.เลย, ปภ.จ.หนองบัวลำภู (LINE 61 ปภ.), [Thai PBS](https://www.thaipbs.or.th/news/content/339679), [LINE TODAY](https://today.line.me/th/v3/article/PG1GLK7), [สยามรัฐ](https://siamrath.co.th/regional/f5485b7f-212d-4893-a25a-a6cf2e1b871b), [มติชน](https://www.matichon.co.th/region/news_4560810)
- Pulkkinen, S., et al. (2019). Pysteps: an open-source Python library for probabilistic precipitation nowcasting (v1.0). *Geosci. Model Dev.*, 12, 4185–4219. https://doi.org/10.5194/gmd-12-4185-2019
- Feldmann, M., et al. (2021). A characterisation of Alpine mesocyclone occurrence. *Weather Clim. Dynam.*, 2, 1225–1244.
- May, R. M., et al. (2022). MetPy: A Meteorological Python Library for Data Analysis and Visualization. *BAMS*, 103, E2273–E2284.
