# mongodb-query

1. Membuat Database academic
use academic;

2. Menampilkan semua collection dan data dalam Database
show collections;
db.department.find();
db.student.find();

3. Membuat atau mengaktifkan Database
use academic;

4. Membuat collection department
db.createCollection(department,
  {
    code : "A001",
    name : "Cross Fox 2017",
    major : "Javascript"
  }
);

OR

db.createCollection(department);
db.department.insert(
  {
    code : "A001",
    name : "Cross Fox 2017",
    major : "Javascript"
  }
);

5. Membuat collection student
db.createCollection(student,
  {
    studentId : "1801403324",
    name : "dgana",
    address : "Jl. Kemang IC no.2",
    "department":
    {
      "$ref" : "department",
      "$id" : ObjectId("58900d79e8469279cb63501f"),
      "$db" : "academic"
    }
  }
);

OR

db.createCollection(student);
db.student.insert(
  {
    studentId : "1801403324",
    name : "dgana",
    address : "Jl. Kemang IC no.2",
    "department":
    {
      "$ref" : "department",
      "$id" : ObjectId("58900d79e8469279cb63501f"),
      "$db" : "academic"
    }
  }
);

6. Melihat struktur collection student
var students = db.student.findOne();
for (var key in students) { print (key) ; }

7. Menginputkan 5 data ke dalam collection department
let bulk = db.department.initializeUnorderedBulkOp();

bulk.insert( { code: "A002", name: "Blanford Fox 2016", major: "Angular JS" } );
bulk.insert( { code: "A003", name: "Arctic Fox 2016", major: "React JS" } );
bulk.insert( { code: "A004", name: "Darwin Fox 2016", major: "Node JS" } );
bulk.insert( { code: "A005", name: "Ethiopian Fox 2017", major: "Mongo DB" } );
bulk.insert( { code: "A006", name: "Fat Fox 2017", major: "Postgres" } );

bulk.execute();

8. Menginputkan 3 data ke dalam collection student beserta reference ke department
db.student.insertMany(
  [
    {
      studentId : "1801403325",
      name : "syanmil",
      address : "Jl. Pondok Indah no.1",
      "department":
      {
        "$ref" : "department",
        "$id" : ObjectId("5890151eede8003d6a36168e"),
        "$db" : "academic"
      }
    },  
    {
      studentId : "1801403326",
      name : "fadly",
      address : "Jl. Puri Indah no.1",
      "department":
      {
        "$ref" : "department",
        "$id" : ObjectId("5890151eede8003d6a36168e"),
        "$db" : "academic"
      }
    },
    {
      studentId : "1801403327",
      name : "timothy",
      address : "Jl. Bintaro no.4",
      "department":
      {
        "$ref" : "department",
        "$id" : ObjectId("589017d0ede8003d6a36168f"),
        "$db" : "academic"
      }
    }
  ]
);

9. Melihat collection student
db.student.find();

10. Menampilkan key name dan address dalam collection student
db.student.find({}, {name:1, address:1});

11. Menampilkan key StudentId, name, dan address dari data student yang mempunyai studentId tertentu
db.student.find({}, {where:{studentId:"1801403324"} name:1, address:1}});

14. Mencari data student dengan name
