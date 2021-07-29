# SQL语句

``` sql
select *from audit_online_register yz where yz.loginid = '15882131277'
select * from audit_online_register yz where yz.rowguid= 'b43b7a25-0a96-40b9-8199-e0fe69b74038';
--项目表通过建设单位账号
select
  xm.ITEMCODE as xmbh,
  xm.itemname as xmmc,
  xm.* 
from
  audit_rs_item_baseinfo xm 
where 
  xm.yzguid in ( select yz.rowguid from audit_online_register yz where yz.loginid= '17780651112');
  -- 更新关联关系，项目表-规划许可-公司表-用户信息表
update audit_rs_item_baseinfo a set a.rowguid=a.rowguid;
update audit_item_ghxk a set a.rowguid=a.rowguid;
update audit_rs_company_baseinfo a set a.rowguid=a.rowguid;
update audit_online_register set rowguid=rowguid where loginid= '18200255226';
--项目表
select xm.yzguid,xm.* from  audit_rs_item_baseinfo xm where xm.itemcode like '1000001597199016%';
select xm.yzguid,xm.* from  audit_rs_item_baseinfo xm where xm.itemname like '%菁蓉滨湖湾%';
--select * from audit_online_register a where a.rowguid='a4e05480-6013-4fb7-8920-9ef26bd70d73';
--select * from audit_rs_company_baseinfo a where a.ORGALEGAL_IDNUMBER='510102196602073211';
select * from c

--规划许可--cardnum--社会信用代码
select * from audit_item_ghxk a where a.xmbh='1000001597199016';
--公司信息
--creditcode--社会信用代码
select * from audit_rs_company_baseinfo a where a.CREDITCODE='91510122572290787E';
--法人身份证
select * from audit_rs_company_baseinfo a where a.ORGALEGAL_IDNUMBER='510122196309162878';
--建设单位
select * from audit_rs_company_baseinfo a where a.organname like '%%';
--中介测绘单位
select * from zjcs_info a where dwqc like '%新都城建勘察%'
select a.rowid,a.* from zjcs_info a where a.yyzzbh='91120116777332442M';
--中介受理明细表
select a.rowid,a.* from t_dchy_zjslmx a where a.zjid='742ac2d1-5617-4f9e-a09e-1a57611f96e0';
--update zjcs_info a set rowguid=rowguid where a.yyzzbh='9151010758758557XL'


--测绘成果问题-Oracle
--预测
select a.rowid,a.* from t_dchy_chcgy a where a.ydchybh='Y2021062300202';
--实测
select a.rowid,a.* from t_dchy_chcg a where a.dchybh='2021061800200';
--测绘成果受理明细
select a.rowid,a.* from b_chcg_slmx a where a.cgid='FCAE2BC4CD0A4E40BBEF5FC767C98BDD';
--业务信息  --取IID
select a.rowid,a.* from ut_dchy_scsh a where a.slmxid='C541A933BDA14D0FE053F203A8C0082E';
select * from t_dchy_chjlfg a where a.slmxid='B59A9B5121D2340AE053F203A8C0156B';

--文件名称规则
--AA_BB_CC_DD.7z
--委托信息
select * from t_dchy_xmsxzjht wt where wt.htid='05AB51E877DB4810BB5B2A2AF82DB3B1';
select * from t_dchy_xmsxzjht wt where wt.htmc like '%成都大润%'
--受理结论
select * from t_dchy_shjl a where a.slmxid='C541A933BCF44D0FE053F203A8C0082E';
--FTP
select * from st_server a;
--二维码
select * from t_dchy_qrcode a where a.dchybh='2021061800200';
select a.*,a.rowid from t_dchy_wsrw_hist a where dchybh = '2021061800200';
--二维码任务表
select a.*,a.rowid from  t_dchy_wsrw a where dchybh = '2021061800200';
--成果质检
select a.*,a.rowid from t_dchy_cgzj a where  a.dchybh = '2021061100103';
select a.*,a.rowid from t_dchy_cgzj a where  a.state=1 and a.dchybh != '';
--并联验收信息没推送到多测合一
select * from t_dchy_cgrk a where a.dchybh = '2020112700101'
select * from t_dchy_cgrk a where a.rowguid = 'da47c8a6-c409-4444-8498-ed606d952453'


--查询委托项目信息
  select decode(d.organname,                                      
                '',                                               
                decode(b.applyname, '', c.username, b.applyname), 
                d.organname) as "yzmc",                         
         a.itemname  as "xmmc",                                 
         a.xmbh      as "xmbh",                                 
         b.xmaddress as "xmdz",                                 
         a.rowguid   as "xmid"                                  
    from audit_rs_item_baseinfo    a,                             
         audit_item_ghxk           b,                             
         audit_online_register     c,                             
         audit_rs_company_baseinfo d                              
   where a.xmbh = b.xmbh(+)                                       
     and a.yzguid = c.rowguid                                     
     and c.idnumber = d.orgalegal_idnumber(+)                     
     and a.itemname like concat(concat('%', ''), '%')             
     and b.cardnum=d.creditcode                                   
     and a.yzguid = 'bb6a2578-62e7-4f52-b697-daa751c9a945'


  select a.htid  as "wtid",                     
       a.htmc  as "wtmc",                       
       a.htje  as "wtje",                       
       a.xzq   as "xzqdm",                      
       b.xzqmc as "xzqmc",                      
       a.xmmc  as "xmmc",                       
       a.type  as "type"                        
  from t_dchy_xmsxzjht a, t_dchy_xzq b            
 where a.xzq = b.xzqdm                            
   and a.yzid = 'bb6a2578-62e7-4f52-b697-daa751c9a945'                                
   and a.htmc like concat(concat('%', ''), '%')   
 order by a.edittime desc
```

