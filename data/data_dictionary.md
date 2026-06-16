# 📊 Dataset Information & Data Dictionary

**⚠️ Data Privacy Notice:** Due to the proprietary and confidential nature of the geotechnical borehole records utilized in this research, the raw `.csv` files have been omitted from this public repository. 

The models in the `notebooks/` directory were trained and strictly validated on data conforming to the structure below. To run the notebooks locally, please format your own SPT datasets to match these exact columns.

### Data Dictionary

| Column Name | Data Type | Description | Unit |
| :--- | :--- | :--- | :--- |
| `Pile_Length_m` | Float | The total embedded length of the driven pile. | Meters (m) |
| `Pile_Size_mm` | Integer | The cross-sectional diameter/width of the pile. | Millimeters (mm) |
| `N60_Shaft` | Float | The depth-averaged, energy-corrected SPT blow count along the pile shaft. | Blows/300mm |
| `N60_Tip` | Float | The energy-corrected SPT blow count at the pile termination depth. | Blows/300mm |
| `Soil_Type` | Categorical | The primary geological classification of the stratum (e.g., Sand, Clay, Silt). | String |
| `Q_gross_kN` | Float | **[TARGET VARIABLE]** The ultimate axial bearing capacity. | Kilonewtons (kN) |

### Sample Dummy Structure
If recreating this pipeline, ensure your CSV headers strictly match:
`Pile_Length_m, Pile_Size_mm, N60_Shaft, N60_Tip, Soil_Type, Q_gross_kN`
`10.5, 300, 14.2, 22.0, Sand, 1250.5`
`8.0, 450, 8.5, 12.0, Clay, 450.0`
