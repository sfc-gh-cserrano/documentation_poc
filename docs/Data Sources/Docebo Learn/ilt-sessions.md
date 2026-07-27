# ILT Sessions & Webinars

> Instructor-Led Training sessions, virtual classrooms (webinars), locations, scheduling, and attendance tracking.

These tables manage the logistics of live/synchronous training: classrooms, session dates, instructor assignments, attendance records, and webinar tool integrations.

**Domains covered**: ILT Sessions (14), Webinars (12), Attendance (1)  
**Total tables**: 27 | **Total columns**: ~350 | **Total FKs**: 8

---

## ER Diagram — Key Tables

```mermaid
erDiagram
    LT_COURSE_SESSION {
        NUMBER id_session PK
        NUMBER id_course FK
        STRING name
        NUMBER min_enroll
        NUMBER max_enroll
    }

    LT_COURSEUSER_SESSION {
        NUMBER id PK
        NUMBER id_session FK
        NUMBER id_user FK
        NUMBER status
        TIMESTAMP date_inscr
    }

    LT_COURSE_SESSION_DATE {
        NUMBER id_date PK
        NUMBER id_session FK
        TIMESTAMP day
        TIMESTAMP time_begin
        TIMESTAMP time_end
    }

    LT_COURSE_SESSION_DATE_ATTENDANCE {
        NUMBER id PK
        NUMBER id_date FK
        NUMBER id_user FK
        NUMBER attendance_status
    }

    LT_COURSE_SESSION_INSTRUCTOR {
        NUMBER id PK
        NUMBER id_session FK
        NUMBER id_user FK
    }

    LT_CLASSROOM {
        NUMBER id PK
        NUMBER id_location FK
        STRING name
        NUMBER capacity
    }

    LT_LOCATION {
        NUMBER id PK
        STRING name
        STRING address
    }

    WEBINAR_SESSION {
        NUMBER id_session PK
        NUMBER id_course
        STRING webinar_tool
    }

    WEBINAR_SESSION_USER {
        NUMBER id PK
        NUMBER id_session FK
        NUMBER id_user FK
    }

    WEBINAR_SESSION_DATE {
        NUMBER id_date PK
        NUMBER id_session FK
        TIMESTAMP day
    }

    WEBINAR_SESSION_DATE_ATTENDANCE {
        NUMBER id PK
        NUMBER id_date FK
        NUMBER id_user FK
    }

    CORE_USER {
        NUMBER idst PK
    }

    LT_COURSE_SESSION ||--o{ LT_COURSEUSER_SESSION : "enrollments"
    CORE_USER ||--o{ LT_COURSEUSER_SESSION : "attends"
    LT_COURSE_SESSION ||--o{ LT_COURSE_SESSION_DATE : "scheduled dates"
    LT_COURSE_SESSION_DATE ||--o{ LT_COURSE_SESSION_DATE_ATTENDANCE : "attendance"
    LT_COURSE_SESSION ||--o{ LT_COURSE_SESSION_INSTRUCTOR : "instructors"
    LT_LOCATION ||--o{ LT_CLASSROOM : "classrooms"
    WEBINAR_SESSION ||--o{ WEBINAR_SESSION_USER : "participants"
    WEBINAR_SESSION ||--o{ WEBINAR_SESSION_DATE : "dates"
    WEBINAR_SESSION_DATE ||--o{ WEBINAR_SESSION_DATE_ATTENDANCE : "attendance"
```

---

## All Tables

### ILT Sessions (14 tables)

| Table | Cols | FKs | Description |
|-------|------|-----|-------------|
| LT_CLASSROOM | 13 | 0 | Physical/virtual classroom definitions |
| LT_COURSEUSER_SESSION | 28 | 1 | User enrollment in ILT sessions |
| LT_COURSE_SESSION | 35 | 1 | ILT session metadata |
| LT_COURSE_SESSION_DATE | 13 | 0 | Session date/time schedule |
| LT_COURSE_SESSION_DATE_ATTENDANCE | 9 | 0 | Per-date attendance records |
| LT_COURSE_SESSION_DATE_CALENDAR_RSVP | 7 | 0 | Calendar RSVP responses |
| LT_COURSE_SESSION_DATE_CALENDAR_SYNC | 8 | 0 | Calendar sync status |
| LT_COURSE_SESSION_DATE_RECORDING | 9 | 0 | Session date recordings |
| LT_COURSE_SESSION_DATE_WEBINAR_SETTING | 10 | 0 | Webinar settings per date |
| LT_COURSE_SESSION_FIELD_VALUE | 7 | 0 | Session custom field values |
| LT_COURSE_SESSION_INSTRUCTOR | 8 | 1 | Session instructor assignments |
| LT_COURSE_SESSION_SHOPIFY_VARIANT | 7 | 0 | Shopify variant mapping |
| LT_LOCATION | 16 | 0 | Physical training locations |
| LT_LOCATION_PHOTO | 8 | 0 | Location photos |

### Webinars (12 tables)

| Table | Cols | FKs | Description |
|-------|------|-----|-------------|
| WEBINAR_ILT_ADDITIONAL_FIELDS_MIGRATION | 7 | 0 | ILT migration fields |
| WEBINAR_ILT_EVENT_MAP | 9 | 0 | ILT-to-webinar event mapping |
| WEBINAR_ILT_MIGRATION_RESULT | 9 | 0 | Migration results |
| WEBINAR_ILT_SESSION_MAP | 8 | 0 | ILT-to-webinar session mapping |
| WEBINAR_SESSION | 21 | 2 | Webinar session metadata |
| WEBINAR_SESSION_DATE | 12 | 0 | Webinar scheduled dates |
| WEBINAR_SESSION_DATE_ATTENDANCE | 9 | 0 | Webinar date attendance |
| WEBINAR_SESSION_DATE_RECORDING | 9 | 0 | Webinar recordings |
| WEBINAR_SESSION_FIELD_VALUE | 7 | 0 | Custom field values for webinar sessions |
| WEBINAR_SESSION_SHOPIFY_VARIANT | 7 | 0 | Shopify variant mapping |
| WEBINAR_SESSION_USER | 22 | 2 | Webinar session user enrollment |
| WEBINAR_TOOL_ACCOUNT | 17 | 1 | Webinar tool account configuration |

### Attendance (1 table)

| Table | Cols | FKs | Description |
|-------|------|-----|-------------|
| ATTENDANCE_SHEET_FIELDS_MAIN | 14 | 0 | Attendance sheet field definitions |

---

## Cross-Domain Relationships

| Source Table | FK Column | Target Domain | Target Table |
|-------------|-----------|---------------|-------------|
| LT_COURSEUSER_SESSION | id_user | [Core Platform](core-platform.md) | CORE_USER |
| LT_COURSE_SESSION | id_course | [Learning](learning.md) | LEARNING_COURSE |
| LT_COURSE_SESSION_INSTRUCTOR | id_user | [Core Platform](core-platform.md) | CORE_USER |
| WEBINAR_SESSION | id_course | [Learning](learning.md) | LEARNING_COURSE |
| WEBINAR_SESSION_USER | id_user | [Core Platform](core-platform.md) | CORE_USER |
| WEBINAR_TOOL_ACCOUNT | id_user | [Core Platform](core-platform.md) | CORE_USER |

---

[Back to README](README.md)
