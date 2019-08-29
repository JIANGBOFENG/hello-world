# hello-world
CREATE DATABASE loan；#建立数据库
use loan； 
CREATE table sum_data(
  policy_code VARCHAR(2),
  num INT,
  total INT ,
PRIMARY KEY (policy_code)

);#建表放贷交易总额分析
CREATE table grade_data(
  grade VARCHAR(2),
  total INTEGER ,
PRIMARY KEY (grade)

);#建表人员信用分析
CREATE table location_data(
  zip_code VARCHAR(20),
  total INT,
PRIMARY KEY (zip_code)

);#建表人员地理位置分析
CREATE table home_data(
  home VARCHAR(20),
  total INTEGER,
PRIMARY KEY (home)

);#建表人员住房分析
CREATE table inc_data(
  inc VARCHAR(20),
  total INTEGER,
PRIMARY KEY (inc)

);#建表人员年收入分析
CREATE table career_data(
  career VARCHAR(20),
  total INTEGER,
PRIMARY KEY (career)
);#建表人员职业分析
CREATE table purpose_data(
  purpose VARCHAR(20),
  total INTEGER,
PRIMARY KEY (purpose)
);#建表人员目的分析
CREATE table alarm_data(
  id VARCHAR(20),
  loan_amnt INTEGER,
  term VARCHAR (20),
  emp_length VARCHAR(20),
  annual_inc FLOAT ,
  zip_code VARCHAR(20),
  purpose VARCHAR (30),
PRIMARY KEY (id)
);#风险预警标准（可调，设置语句就好，先drop table alarm_data;然后再新建CREATE table alarm_data(）
