# LMSApplication
Leave Management System


# MYSQL 
create database lms;
use lms;
CREATE TABLE manager (
    mid INT PRIMARY KEY AUTO_INCREMENT,
    mname VARCHAR(100) NOT NULL,
    memail VARCHAR(100) UNIQUE NOT NULL,
    mpassword VARCHAR(255) NOT NULL,
    mdept VARCHAR(50),
    mjoining_date DATE
);

CREATE TABLE employee (
    eid INT PRIMARY KEY AUTO_INCREMENT,
    ename VARCHAR(100) NOT NULL,
    eemail VARCHAR(100) UNIQUE NOT NULL,
    epassword VARCHAR(255) NOT NULL,
    edept VARCHAR(50),
    ejoining_date DATE,
    manager_id INT,
    FOREIGN KEY (manager_id)
    REFERENCES manager(mid)
);


CREATE TABLE leavetype (
    ltid INT PRIMARY KEY AUTO_INCREMENT,
    leavename VARCHAR(50) UNIQUE NOT NULL
);

CREATE TABLE leave_balance (
    lbid INT PRIMARY KEY AUTO_INCREMENT,
    eid INT NOT NULL,
    ltid INT NOT NULL,
    availabledays INT DEFAULT 0,
    FOREIGN KEY (eid)
    REFERENCES employee(eid),
    FOREIGN KEY (ltid)
    REFERENCES leavetype(ltid),
    UNIQUE(eid, ltid)
);


CREATE TABLE leave_request (
    lid INT PRIMARY KEY AUTO_INCREMENT,
    eid INT NOT NULL,
    ltid INT NOT NULL,
    from_date DATE NOT NULL,
    to_date DATE NOT NULL,
    reason VARCHAR(500),
    status varchar(20) DEFAULT 'PENDING',
    applied_date DATE NOT NULL,
    approved_date DATE,
    FOREIGN KEY (eid)
    REFERENCES employee(eid),
    FOREIGN KEY (ltid)
    REFERENCES leavetype(ltid)

);

 

 

INSERT INTO manager (mname, memail, mpassword, mdept, mjoining_date) VALUES
('Sai Srinivas', 'srinivas@gmail.com', 'Srinu@12345', 'IT', '2022-01-10'),
('Mopidevi Balaji', 'balaji@gmail.com', 'Balaji@12345', 'IT', '2021-06-15');

 

 

INSERT INTO employee (ename, eemail, epassword, edept, ejoining_date, manager_id) VALUES
('Girish', 'girish@gmail.com', 'girish1234', 'Java Developer', '2023-03-01', 1),
('Jahanvi', 'jahnvi@gmail.com', 'jahnvi12345', 'Frontend', '2023-04-10', 2);

 

 

INSERT INTO leavetype (leavename) VALUES
('Casual Leave'),
('Sick Leave'),
('Earned Leave'),
('Loss of Pay');

INSERT INTO leave_balance (eid, ltid, availabledays) VALUES
(1,1,12),(1,2,10),(1,3,15),(1,4,5),
(2,1,12),(2,2,10),(2,3,15),(2,4,5);
