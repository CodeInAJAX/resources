# Database Directory

This directory contains the database schema represented through an Entity-Relationship Diagram (ERD). The schema is designed and managed using DB Diagram, a tool for visualizing and documenting database structures.

## Contents
- **ERD File**: The database schema is shared as a DB Diagram file, which can be opened and edited using the DB Diagram platform.
- **Exported Photo**: A visual representation of the ERD is provided as an image file for quick reference.
- **Shareable Link**: A link to the DB Diagram project is included, allowing collaborators to view or edit the schema directly on the platform.

## Usage
1. **View the ERD**: Open the exported photo file to quickly understand the database structure.
2. **Edit the Schema**: Use the shareable link to access the DB Diagram project and make modifications as needed.
3. **Collaborate**: Share the link with team members to collaborate on the schema design.

## Notes
- Ensure you have access to the DB Diagram platform to edit the schema.
- Keep the exported photo file updated whenever changes are made to the schema.
- [DB Diagram](https://dbdiagram.io/d/CodeinAjax-6818331d1ca52373f56e9cae) Only View
- The ERD (Entity Relationship Diagram) can be viewed in the following file:
File location: `erd/ERD.png` 

Alternatively, it can be visualized using the syntax DB Diagram below to describe the ERD structure. 
```
enum Role {
  ADMIN
  MENTOR
  STUDENT
}

enum Gender {
  MALE
  FEMALE
} 

Table users {
  id         uuid [pk]
  name       varchar
  email      varchar [unique]
  password   varchar
  role       Role // should be one of: 'ADMIN', 'MENTOR', 'STUDENT'
  created_at timestamp
  updated_at timestamp
  deleted_at timestamp [null]
}

Table courses {
  id          uuid [pk]
  title       varchar
  description text
  thumbnail   text // optional course image
  price       int   // in cents or smallest currency unit (e.g. 10000 = Rp 100.00)
  mentor_id   uuid [ref: > users.id]
  created_at  timestamp
  updated_at  timestamp
}

Table profiles {
  id      uuid [pk]
  gender  Gender 
  about     text [null]
  photo   varchar 
  user_id uuid [ref: - users.id]
  created_at  timestamp
  updated_at  timestamp
}

Table enrollments {
  id          uuid [pk]
  course_id   uuid [ref: > courses.id]
  student_id  uuid [ref: > users.id]
  enrolled_at timestamp
  status      varchar // optional: 'ACTIVE', 'COMPLETED'
}

Table lessons {
  id          uuid [pk]
  course_id   uuid [ref: > courses.id]
  title       varchar
  description text
  video_link  text
  duration    int // in seconds (optional)
  order_num   int // for lesson ordering
  created_at  timestamp
}

//  Optional
Table payments {
  id           uuid [pk]
  student_id   uuid [ref: > users.id]
  course_id    uuid [ref: > courses.id]
  amount       int   // in cents or smallest currency unit
  payment_date timestamp
  status       varchar // e.g. 'PENDING', 'SUCCESS', 'FAILED'
  payment_method varchar // e.g. 'CREDIT_CARD', 'BANK_TRANSFER', 'EWALLET'
}

Table ratings {
  id         uuid [pk]
  user_id    uuid [ref: > users.id]
  course_id  uuid [ref: > courses.id]
  rating     int 
  comment     text [null] 
  created_at timestamp

  Indexes {
    (user_id, course_id) [unique]
  }
}
```