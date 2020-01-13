UNIT-TYPE-VALUE
===============

This file defines the semantic for KNoT data types and unities used by KNoT data sources. 

+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
|          KNoT Type ID          | | KNoT Type ID     |          KNoT Unit          | | KNoT Unit     |      Value Type       |
|                                | | Value            |                             | | Value         |                       |
+================================+====================+=============================+=================+=======================+
| KNOT_TYPE_ID_NONE              | 0x0000             | KNOT_UNIT_NOT_APPLICABLE    | 0x00            | KNOT_VALUE_TYPE_RAW   |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_VOLTAGE           | 0x0001             | | KNOT_UNIT_VOLTAGE_V       | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_VOLTAGE_MV      | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_VOLTAGE_KV      | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_CURRENT           | 0x0002             | | KNOT_UNIT_CURRENT_A       | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_CURRENT_MA      | | 0x02          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_RESISTENCE        | 0x0003             | KNOT_UNIT_RESISTENCE_OHM    | 0x01            | KNOT_VALUE_TYPE_INT   |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_POWER             | 0x0004             | | KNOT_UNIT_POWER_W         | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_POWER_KW        | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_POWER_MW        | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_TEMPERATURE       | 0x0005             | | KNOT_UNIT_TEMPERATURE_C   | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_TEMPERATURE_F   | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_TEMPERATURE_K   | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_RELATIVE_HUMIDITY | 0x0006             | KNOT_UNIT_RELATIVE_HUMIDITY | 0x01            | KNOT_VALUE_TYPE_INT   |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_LUMINOSITY        | 0x0007             | | KNOT_UNIT_LUMINOSITY_LM   | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_LUMINOSITY_CD   | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_LUMINOSITY_LX   | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_TIME              | 0x0008             | | KNOT_UNIT_TIME_S          | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_TIME_MS         | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_TIME_US         | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_MASS              | 0x0009             | | KNOT_UNIT_MASS_KG         | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_MASS_G          | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_MASS_LB         | | 0x03          |                       |
|                                |                    | | KNOT_UNIT_MASS_OZ         | | 0x04          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_PRESSURE          | 0x000A             | | KNOT_UNIT_PRESSURE_PA     | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_PRESSURE_PSI    | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_PRESSURE_BAR    | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_DISTANCE          | 0x000B             | | KNOT_UNIT_DISTANCE_M      | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_DISTANCE_CM     | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_DISTANCE_MI     | | 0x03          |                       |
|                                |                    | | KNOT_UNIT_DISTANCE_IN     | | 0x04          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_ANGLE             | 0x000C             | | KNOT_UNIT_ANGLE_RAD       | | 0x01          | KNOT_VALUE_TYPE_FLOAT |
|                                |                    | | KNOT_UNIT_ANGLE_DEGREE    | | 0x02          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_VOLUME            | 0x000D             | | KNOT_UNIT_VOLUME_L        | | 0x01          | KNOT_VALUE_TYPE_FLOAT |
|                                |                    | | KNOT_UNIT_VOLUME_ML       | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_VOLUME_FLOZ     | | 0x03          |                       |
|                                |                    | | KNOT_UNIT_VOLUME_GAL      | | 0x04          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_AREA              | 0x000E             | | KNOT_UNIT_AREA_M2         | | 0x01          | KNOT_VALUE_TYPE_FLOAT |
|                                |                    | | KNOT_UNIT_AREA_HA         | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_AREA_AC         | | 0x03          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_RAIN              | 0x000F             | KNOT_UNIT_RAIN_MM           | 0x01            | KNOT_VALUE_TYPE_FLOAT |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_DENSITY           | 0x0010             | KNOT_UNIT_DENSITY_KGM3      | 0x01            | KNOT_VALUE_TYPE_FLOAT |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_LATITUDE          | 0x0011             | KNOT_UNIT_LATITUDE_DEGREE   | 0x01            | KNOT_VALUE_TYPE_FLOAT |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_LONGITUDE         | 0x0012             | KNOT_UNIT_LONGITUDE_DEGREE  | 0x01            | KNOT_VALUE_TYPE_FLOAT |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_SPEED             | 0x0013             | | KNOT_UNIT_SPEED_MS        | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_SPEED_CMS       | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_SPEED_KMH       | | 0x03          |                       |
|                                |                    | | KNOT_UNIT_SPEED_MIH       | | 0x04          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_VOLUMEFLOW        | 0x0014             | | KNOT_UNIT_VOLUMEFLOW_M3S  | | 0x01          | KNOT_VALUE_TYPE_FLOAT |
|                                |                    | | KNOT_UNIT_VOLUMEFLOW_SCMM | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_VOLUMEFLOW_LS   | | 0x03          |                       |
|                                |                    | | KNOT_UNIT_VOLUMEFLOW_LM   | | 0x04          |                       |
|                                |                    | | KNOT_UNIT_VOLUMEFLOW_FT3S | | 0x05          |                       |
|                                |                    | | KNOT_UNIT_VOLUMEFLOW_GALM | | 0x06          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_ENERGY            | 0x0015             | | KNOT_UNIT_ENERGY_J        | | 0x01          | KNOT_VALUE_TYPE_INT   |
|                                |                    | | KNOT_UNIT_ENERGY_NM       | | 0x02          |                       |
|                                |                    | | KNOT_UNIT_ENERGY_WH       | | 0x03          |                       |
|                                |                    | | KNOT_UNIT_ENERGY_KWH      | | 0x04          |                       |
|                                |                    | | KNOT_UNIT_ENERGY_CAL      | | 0x05          |                       |
|                                |                    | | KNOT_UNIT_ENERGY_KCAL     | | 0x06          |                       |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| KNOT_TYPE_ID_ACCELERATION      | 0X0016             | KNOT_UNIT_ACCELERATION_MS2  | 0X01            | KNOT_VALUE_TYPE_INT   |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
| | TypeIDs for logical units    | |                  | |                           | |               | |                     |
| | KNOT_TYPE_ID_PRESENCE        | | 0xFFF0           | | KNOT_UNIT_NOT_APPLICABLE  | | 0x00          | | KNOT_VALUE_TYPE_BOOL|
| | KNOT_TYPE_ID_SWITCH          | | 0xFFF1           | | KNOT_UNIT_NOT_APPLICABLE  | | 0x00          | | KNOT_VALUE_TYPE_BOOL|
| | KNOT_TYPE_ID_COMMAND         | | 0xFFF2           | | KNOT_UNIT_NOT_APPLICABLE  | | 0x00          | | KNOT_VALUE_TYPE_RAW |
| | KNOT_TYPE_ID_ANALOG          | | 0xFF10           | | KNOT_UNIT_NOT_APPLICABLE  | | 0x00          | | KNOT_VALUE_TYPE_INT |
| | KNOT_TYPE_ID_INVALID         | | 0xFFFF           | | KNOT_UNIT_NOT_APPLICABLE  | | 0x00          | | KNOT_VALUE_TYPE_RAW |
+--------------------------------+--------------------+-----------------------------+-----------------+-----------------------+
