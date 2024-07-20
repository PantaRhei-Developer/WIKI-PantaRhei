# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)
    - [複合キーの決定](#複合キーの決定)
    - [テーブル作成](#テーブル作成)

# 0. 結論
複合キーを決定した．
データレイクとなるテーブルの作成をした．

# 1. 概要
[INTERN-187: スクレイピングデータを入れるテーブルを作成完了](https://pantarhei-hub.atlassian.net/browse/INTERN-187)
 

# 2. ワークログ
## 2.0. 複合キーの決定
企業と求人の両方を区別できるようにすることを目的とし，データレイクの複合キーを決定した．

複合キーは以下のカラムである．

```
###企業を区別する複合キー###
company_location

###求人を区別する複合キー###
job_content, job_annual_income, job_start_date，job_end_date
```

## 2.1. テーブル作成
cloud shellでcloud SQLに接続し，以下のようにテーブル(hellowork_datalake)を作成する．

```
CREATE OR REPLACE FUNCTION update_updated_at()
RETURNS TRIGGER AS $$
BEGIN
  NEW.updated_at = CURRENT_TIMESTAMP;
  RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_updated_at_trigger
BEFORE UPDATE ON hellowork_datalake
FOR EACH ROW
EXECUTE FUNCTION update_updated_at();

CREATE TABLE hellowork_datalake(
    id BIGINT,
    source_job_url TEXT,
    corporate_number TEXT,
    job_start_date TEXT,
    job_end_date TEXT,
    job_content TEXT,
    job_content_summary TEXT,
    job_salary TEXT,
    job_annual_income TEXT,
    job_employment_type TEXT,
    job_application_steps TEXT,
    job_application_contact_info TEXT,
    company_introduction TEXT,
    job_qualification_requirements TEXT,
    company_recruit_tel TEXT,
    company_recruit_responsible TEXT,
    company_recruit_email TEXT,
    company_address TEXT,
    company_business TEXT,
    company_capital TEXT,
    company_employee TEXT,
    company_establish_year TEXT,
    company_fax TEXT,
    company_hp_url TEXT,
    company_industry TEXT,
    company_location TEXT,
    company_name TEXT,
    company_name_kat_notation TEXT,
    company_postalcode TEXT,
    company_representative TEXT,
    info_source TEXT,
    get_time TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP,
    cleansing_flag SMALLINT,
    PRIMARY KEY (company_location, job_content, job_annual_income, job_start_date, job_end_date)
);
```
