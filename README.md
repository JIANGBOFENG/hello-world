# hello-world
/*实时流计算服务：*/
/*创建数据流，数据源从DIS中流入*/
create source stream loan_source(
id STRING,
member_id STRING,
loan_amnt INT,
funded_amnt FLOAT,
funded_amnt_inv FLOAT,
term STRING,
int_rate FLOAT,
installment FLOAT,
grade STRING,
sub_grade STRING,
emp_length STRING,
home_ownership STRING,
annual_inc FLOAT,
verification_status STRING,
issue_d STRING,
loan_status STRING,
pymnt_plan STRING,
url STRING,
purpose STRING,
zip_code STRING,
addr_atate STRING,
dti FLOAT,
delinq_2yrs INT,
earliest_cr_line STRING,
inq_last_6mths INT,
mths_since_last_delinq STRING,
mths_since_last_record STRING,
open_acc INT,
pub_rec INT,
revol_bal FLOAT,
revol_util STRING,
total_acc INT,
initial_list_status STRING,
out_prncp FLOAT,
out_prncp_inv FLOAT,
total_pymnt FLOAT,
total_pymnt_inv FLOAT,
total_rec_prncpn FLOAT,
total_rec_int FLOAT,
total_rec_late_fee FLOAT,
recoveris FLOAT,
collection_recovery_fee float,
last_pymnt_d STRING,
last_pymnt_amnt FLOAT,
next_pymnt_d STRING,
last_credit_pull_d STRING,
collections_12_mths_ex_med int,
mths_since_last_major_derog STRING,
policy_code STRING
)
with(
type="dis",
region="cn-north-1",//   这里是要填dis所在区域
CHANNEL="dis-Ch9x",//    这里是要填申请的dis通道名称，以具体名称为准
PARTITION_COUNT="1",
encode="csv",
FIELD_DELIMITER=","
);

/*创建输出流，结果输入到RDS数据库中*/
/*-----总放款交易金额分析---------*/
CREATE SINK STREAM sum_data(
policy_code STRING,
num int,
total int 
)
WITH(
type="rds",
USERNAME="root",//   云数据库的用户名
PASSWORD="C5-team4",//   这里要云数据库MySQL的登录密码
db_url="mysql://192.168.0.74:3306/loan",// 填入云数据库MySQL的内网IP：端口/数据库名称
TABLE_NAME="sum_data",//  填入遗传建数据库下表名称
PRIMARY_KEY="policy_code"
);

insert into sum_data
select policy_code,count(policy_code) as num,sum(loan_amnt) as total FROM
loan_source group by policy_code;

/*创建输出流，结果输入到rds数据库中*/
/*---------人员信用等级分布--------*/
CREATE SINK STREAM grade_data(
  grade STRING,
  total INTEGER 
)
WITH(
type="rds",
USERNAME="root",//   云数据库的用户名
PASSWORD="C5-team4",//   这里要云数据库MySQL的登录密码
DB_URL="mysql://192.168.0.74:3306/loan",// 填入云数据库MySQL的内网IP：端口/数据库名称
TABLE_NAME="grade_data",//  填入已建数据库下表名称
PRIMARY_KEY="grade"
);
