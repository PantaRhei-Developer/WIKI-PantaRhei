# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)

# 0. 結論
insert実装にすることで，主キーの必要がなくなったため，primary keyの設定を行う行を削除した．
また，トリガーの定義と追加をすることで，updated_atの実装に成功．実際にUpdateを一部行い，テストした結果，成功した．

```
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
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    cleansing_flag SMALLINT
);


CREATE OR REPLACE FUNCTION update_updated_at()
RETURNS TRIGGER AS $$
BEGIN
    NEW.updated_at = CURRENT_TIMESTAMP;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;


CREATE TRIGGER trigger_update_updated_at
BEFORE UPDATE ON hellowork_datalake
FOR EACH ROW
EXECUTE FUNCTION update_updated_at();
```

# 1. 概要
[INTERN-243: insertに合わせてテーブル作成するsql文の変更完了 ](https://remotesalesproject.atlassian.net/browse/INTERN-243)

# 2. ワークログ 
