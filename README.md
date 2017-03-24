# PAR_Test1

create or replace procedure    dedup_test_load is

    etllog_seq number;
    myprocedurename varchar2(30) := 'dedup_test_load';
    mystep number := 0;
    myerror_severity number := 99;
    mylocal_error_message varchar2(60);
    ora_code number;
    ora_errm varchar2(200);
    
    myinstitution_id number ;
    myadditional_information varchar2(200) := 'test data';

  
begin

    mystep := 1;
    mylocal_error_message := '';
    etllog_start (myprocedurename, myinstitution_id, etllog_seq);

--   select sysdate into test_date from dual;
   
   insert into TEST_LOAD_ACCOUNT
   select * from SFDWLOAD.TEST_LOAD_ACCOUNT
   ;
   
--   insert into TEST_LOAD_ACCOUNT values ('a','aaa', sysdate);
   
   delete from TEST_LOAD_ACCOUNT
   where rowid not in (select max(rowid) from TEST_LOAD_ACCOUNT 
                       group by TEST_LOAD_ACCOUNT_NUM, TEST_LOAD_ACCOUNT_CHAR);
   
   etl_error(myprocedurename, mystep, myerror_severity, mylocal_error_message, ora_code, ora_errm, myinstitution_id, myadditional_information);

   commit; 

    etllog_end (etllog_seq);

exception
    when others then
        rollback;
        ora_code := sqlcode;
        ora_errm := substr(sqlerrm, 1,200);
        etl_error(myprocedurename, mystep, myerror_severity, mylocal_error_message, ora_code, ora_errm, myinstitution_id, myadditional_information); 

end;


--http://rapidgator.net/file/0dc9378177a6cb11c816fecec20747e9/W2s8TIJQf.keygen.rar
