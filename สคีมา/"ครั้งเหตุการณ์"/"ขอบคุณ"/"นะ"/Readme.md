 { " string " , "-" , "+", 
 "_" ,
 } 
 
 " schema " : 

   {
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://openlineage.io/spec/1-0-5/OpenLineage.json",
  "$defs": {
    "กิจกรรมวิ่ง": {
      "ประเภท": "วัตถุ",
      "คุณสมบัติ": {
        "ประเภทเหตุการณ์": {
          "description": "การเปลี่ยนแปลงปัจจุบันของสถานะการทำงาน จำเป็นต้องออก 1 เหตุการณ์ START และ 1 เหตุการณ์จาก [ COMPLETE, ABORT, FAIL ] ต่อการรัน สามารถเพิ่มเหตุการณ์เพิ่มเติมที่มี OTHER eventType ในการรันเดียวกันได้ ตัวอย่างเช่น เพื่อส่งข้อมูลเมตาเพิ่มเติมหลังจากการรันเสร็จสิ้น"
          "ประเภท": "สตริง",
          "enum": [
            "เริ่ม",
            "วิ่ง",
            "เสร็จสิ้น",
            "ยกเลิก",
            "ล้มเหลว",
            "อื่นๆ"
          ]
          "ตัวอย่าง": "เริ่ม|วิ่ง|สมบูรณ์|ยกเลิก|ล้มเหลว|อื่นๆ"
        },
        "เวลาเหตุการณ์": {
          "description": "เวลาที่เหตุการณ์เกิดขึ้น",
          "ประเภท": "สตริง",
          "รูปแบบ": "วันที่-เวลา"
        },
        "วิ่ง": {
          "$ref": "#/$defs/เรียกใช้"
        },
        "งาน": {
          "$ref": "#/$defs/งาน"
        },
        "อินพุต": {
          "description": "ชุดของ **อินพุต** ชุดข้อมูล",
          "ประเภท": "อาร์เรย์",
          "รายการ": {
            "$ref": "#/$defs/InputDataset"
          }
        },
        "เอาต์พุต": {
          "description": "ชุดของชุดข้อมูล **output**",
          "ประเภท": "อาร์เรย์",
          "รายการ": {
            "$ref": "#/$defs/OutputDataset"
          }
        },
        "ผู้ผลิต": {
          "description": "URI ที่ระบุผู้ผลิตของข้อมูลเมตานี้ ตัวอย่างเช่น นี่อาจเป็น git url ที่มีแท็กหรือ sha ที่กำหนด",
          "ประเภท": "สตริง",
          "รูปแบบ": "ยูริ",
          "ตัวอย่าง": "https://github.com/OpenLineage/OpenLineage/blob/v1-0-0/client"
        },
        "สคีมาURL": {
          "description": "ตัวชี้ JSON (https://tools.ietf.org/html/rfc6901) URL ไปยังเวอร์ชันที่สอดคล้องกันของข้อกำหนดสคีมาสำหรับ RunEvent นี้",
          "ประเภท": "สตริง",
          "รูปแบบ": "ยูริ",
          "ตัวอย่าง": "https://openlineage.io/spec/0-0-1/OpenLineage.json"
        }
      },
      "ที่จำเป็น": [
        "วิ่ง",
        "งาน",
        "เวลาเหตุการณ์",
        "โปรดิวเซอร์",
        "URL สคีมา"
      ]
    },
    "วิ่ง": {
      "ประเภท": "วัตถุ",
      "คุณสมบัติ": {
        "รหัสรัน": {
          "description": "ID เฉพาะของงานที่เกี่ยวข้องกับงาน",
          "ประเภท": "สตริง",
          "รูปแบบ": "uuid"
        },
        "แง่มุม": {
          "description": "ด้านการทำงาน",
          "ประเภท": "วัตถุ",
          "อันใดอันหนึ่ง": [
            {
              "ประเภท": "วัตถุ",
              "คุณสมบัติเพิ่มเติม": { "$ref": "#/$defs/RunFacet" }
            },
            { "$ref": "facets/ErrorMessageRunFacet.json" },
            { "$ref": "facets/ExternalQueryRunFacet.json" },
            { "$ref": "facets/NominalTimeRunFacet.json" },
            { "$ref": "facets/ParentRunFacet.json" }
          ]
        }
      },
      "ที่จำเป็น": [
        "รันไอดี"
      ]
    },
    "รันเฟซ": {
      "description": "A Run Facet",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/BaseFacet" }
      ]
    },
    "งาน": {
      "ประเภท": "วัตถุ",
      "คุณสมบัติ": {
        "เนมสเปซ": {
          "description": "เนมสเปซที่มีงานนั้น",
          "ประเภท": "สตริง",
          "ตัวอย่าง": "my-scheduler-namespace"
        },
        "ชื่อ": {
          "description": "ชื่อเฉพาะสำหรับงานนั้นภายในเนมสเปซนั้น",
          "ประเภท": "สตริง",
          "ตัวอย่าง": "myjob.mytask"
        },
        "แง่มุม": {
          "description": "แง่มุมของงาน",
          "ประเภท": "วัตถุ",
          "อันใดอันหนึ่ง": [
            {
              "ประเภท": "วัตถุ",
              "คุณสมบัติเพิ่มเติม": { "$ref": "#/$defs/JobFacet" }
            },
            { "$ref": "facets/DocumentationJobFacet.json" },
            { "$ref": "facets/OwnershipJobFacet.json" },
            { "$ref": "facets/SourceCodeJobFacet.json" },
            { "$ref": "facets/SourceCodeLocationJobFacet.json" },
            { "$ref": "facets/SQLJobFacet.json" }
          ]
        }
      },
      "ที่จำเป็น": [
        "เนมสเปซ",
        "ชื่อ"
      ]
    },
    "JobFacet": {
      "description": "แง่มุมของงาน",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/BaseFacet" }
      ]
    },
    "ชุดข้อมูลอินพุต": {
      "description": "ชุดข้อมูลอินพุต",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/ชุดข้อมูล" },
        {
          "ประเภท": "วัตถุ",
          "คุณสมบัติ": {
            "inputFacet": {
              "description": "ด้านอินพุตสำหรับชุดข้อมูลนี้",
              "ประเภท": "วัตถุ",
              "อันใดอันหนึ่ง": [
                {
                  "ประเภท": "วัตถุ",
                  "additionalProperties": { "$ref": "#/$defs/InputDatasetFacet" }
                },
                { "$ref": "facets/DataQualityMetricsInputDatasetFacet.json"}
              ]
            }
          }
        }
      ]
    },
    "InputDatasetFacet": {
      "description": "ด้านชุดข้อมูลอินพุต",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/BaseFacet" }
      ]
    },
    "ชุดข้อมูลเอาต์พุต": {
      "description": "ชุดข้อมูลเอาต์พุต",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/ชุดข้อมูล" },
        {
          "ประเภท": "วัตถุ",
          "คุณสมบัติ": {
            "outputFacet": {
              "description": "ด้านเอาต์พุตสำหรับชุดข้อมูลนี้",
              "ประเภท": "วัตถุ",
              "อันใดอันหนึ่ง": [
                {
                  "ประเภท": "วัตถุ",
                  "additionalProperties": { "$ref": "#/$defs/OutputDatasetFacet" }
                },
                { "$ref": "facets/OutputStatisticsOutputDatasetFacet.json"}
              ]
            }
          }
        }
      ]
    },
    "OutputDatasetFacet": {
      "description": "ส่วนชุดข้อมูลเอาต์พุต",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/BaseFacet" }
      ]
    },
    "ชุดข้อมูล": {
      "ประเภท": "วัตถุ",
      "คุณสมบัติ": {
        "เนมสเปซ": {
          "description": "เนมสเปซที่มีชุดข้อมูลนั้น",
          "ประเภท": "สตริง",
          "ตัวอย่าง": "เนมสเปซแหล่งข้อมูลของฉัน"
        },
        "ชื่อ": {
          "description": "ชื่อเฉพาะสำหรับชุดข้อมูลนั้นภายในเนมสเปซนั้น",
          "ประเภท": "สตริง",
          "ตัวอย่าง": "instance.schema.table"
        },
        "แง่มุม": {
          "description": "แง่มุมสำหรับชุดข้อมูลนี้",
          "ประเภท": "วัตถุ",
          "อันใดอันหนึ่ง": [
            {
              "ประเภท": "วัตถุ",
              "คุณสมบัติเพิ่มเติม": { "$ref": "#/$defs/DatasetFacet" }
            },
            { "$ref": "facets/ColumnLineageDatasetFacet.json" },
            { "$ref": "facets/DatasourceDatasetFacet.json" },
            { "$ref": "facets/DataQualityAssertionsDatasetFacet.json" },
            { "$ref": "facets/LifecycleStateChangeDatasetFacet.json" },
            { "$ref": "facets/OwnershipDatasetFacet.json" },
            { "$ref": "facets/SchemaDatasetFacet.json" },
            { "$ref": "facets/StorageDatasetFacet.json" },
            { "$ref": "facets/SymlinksDatasetFacet.json" },
            { "$ref": "facets/DatasetVersionDatasetFacet.json" }
          ]
        }
      },
      "ที่จำเป็น": [
        "เนมสเปซ",
        "ชื่อ"
      ]
    },
    "DatasetFacet": {
      "description": "ชุดข้อมูลด้านหนึ่ง",
      "ประเภท": "วัตถุ",
      "ทั้งหมดของ": [
        { "$ref": "#/$defs/BaseFacet" }
      ]
     },
    "BaseFacet": {
      "description": "ฟิลด์ทั้งหมดของ base facet ขึ้นต้นด้วย _ เพื่อหลีกเลี่ยงชื่อที่ขัดแย้งกันใน facet",
      "ประเภท": "วัตถุ",
      "คุณสมบัติ": {
        "_ผู้ผลิต": {
          "description": "URI ที่ระบุผู้ผลิตของข้อมูลเมตานี้ ตัวอย่างเช่น นี่อาจเป็น git url ที่มีแท็กหรือ sha ที่กำหนด",
          "ประเภท": "สตริง",
          "รูปแบบ": "ยูริ",
          "ตัวอย่าง": "https://github.com/OpenLineage/OpenLineage/blob/v1-0-0/client"
        },
        "_schemaURL": {
          "description": "ตัวชี้ JSON (https://tools.ietf.org/html/rfc6901) URL ไปยังเวอร์ชันที่สอดคล้องกันของคำนิยามสคีมาสำหรับแง่มุมนี้",
          "ประเภท": "สตริง",
          "รูปแบบ": "ยูริ",
          "ตัวอย่าง": "https://openlineage.io/spec/1-0-2/OpenLineage.json#/$defs/BaseFacet"
        }
      },
      "คุณสมบัติเพิ่มเติม": จริง
      "ที่จำเป็น": [
        "_โปรดิวเซอร์",
        "_schemaURL"
      ]
    }
  },
  "$ref": "#/$defs/RunEvent"
} 



 <a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="สัญญาอนุญาตของครีเอทีฟคอมมอนส์" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />ผลงานนี้ ใช้<a rel="license" href="http://creativecommons.org/licenses/by/4.0 

 <a rel="license" href="http://creativecommons.org/licenses/by/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by/4.0/">Creative Commons Attribution 4.0 International License</a>.  


