//SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract university{
struct college {
string name;
address collegeAddress;
string collegeregno;
}
struct student{
uint ID;
string name;
uint256 phoneno;
string coursename;
address collegeAddress;
}
address private admin;
college private college1;
student[] public students;
bool canAdd;
modifier onlymodifier() {
require(msg.sender == admin, "admin: Only owner can call");
_;
}
constructor() {
admin = msg.sender;
}
mapping(address=>college)public colleges;
function addcollege(string memory _name,
address _collegeAddress,
string memory _collegeregno) public {
// 1. Add new college to blockchain - constructor (onlyowner)
// Allow permission by default
colleges[_collegeAddress].name=_name;
colleges[_collegeAddress].collegeAddress=_collegeAddress;
colleges[_collegeAddress].collegeregno=_collegeregno;
}
function blockcollegetoAddnewstudent(address _collegeAddress) public {
_collegeAddress=_collegeAddress;
canAdd= false;
}
function unblockcollegetoAddnewstudent(address _collegeAddress) public {
_collegeAddress=_collegeAddress;
canAdd= true;
}
// can anyone add new student or only admin
function addstudent(uint _ID,uint256 _phoneno, string memory _name, string memory _coursename, address _collegeAddress) public {
// check if college can add new student
require(canAdd == true, "college: should have privilege to add new students");
// Hardcode customer id or Counter
// Hardcode students id or Counter
students.push(student({ID: _ID,phoneno: _phoneno, name: _name,coursename:_coursename, collegeAddress: _collegeAddress}));
}
function studentInfoByID(uint _ID) view public returns(string memory, string memory, address,uint){
//view students details
return(students[_ID].name,
students[_ID].coursename,
students[_ID].collegeAddress,
students[_ID].phoneno);
}string newcourse;
function changestudentcourse(uint _ID,string memory _name, string memory _newcourse, address _collegeAddress,uint _phoneno)public
{_ID=_ID;
_name=_name;
_newcourse=_newcourse;
_collegeAddress=_collegeAddress;
_phoneno=_phoneno;
}
}
