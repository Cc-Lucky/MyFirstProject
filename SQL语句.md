select yz.rowid,yz.* from audit_online_register yz where yz.loginid= '13880774345';
select * from audit_online_register yz where yz.rowguid= 'f5462077-f84f-41e9-a429-16684c1c7b99';

--项目表通过建设单位账号
select
  xm.ITEMCODE as xmbh,
  xm.itemname as xmmc,
  xm.* 
from
  audit_rs_item_baseinfo xm 
where
  xm.yzguid in ( select yz.rowguid from audit_online_register yz where yz.loginid= '13541387530');
-- 更新关联关系，项目表-规划许可-公司表-用户信息表
update audit_rs_item_baseinfo a set a.rowguid=a.rowguid;
update audit_item_ghxk a set a.rowguid=a.rowguid;
update audit_rs_company_baseinfo a set a.rowguid=a.rowguid;
update audit_online_register set rowguid=rowguid where loginid= '13880774345';
--项目表
select xm.yzguid,xm.* from  audit_rs_item_baseinfo xm where xm.itemcode like '1000001343930471%';
select xm.yzguid,xm.* from  audit_rs_item_baseinfo xm where xm.itemname like '%住宅、统筹住房及配套设施项目%';
--select * from audit_online_register a where a.rowguid='a4e05480-6013-4fb7-8920-9ef26bd70d73';
--select * from audit_rs_company_baseinfo a where a.ORGALEGAL_IDNUMBER='510102196602073211';
select * from c

--规划许可--cardnum--社会信用代码
select * from audit_item_ghxk a where a.xmbh='1000001343930471';
--公司信息
--creditcode--社会信用代码
select * from audit_rs_company_baseinfo a where a.CREDITCODE='91510107MAACEPLX42';
--法人身份证
select * from audit_rs_company_baseinfo a where a.ORGALEGAL_IDNUMBER='510122196309162878';
--建设单位
select * from audit_rs_company_baseinfo a where a.organname like '%中国建筑材料工业%';
--中介测绘单位
select a.rowid,a.* from zjcs_info a where dwqc like '%吉地%'
select a.rowid,a.* from zjcs_info a where a.yyzzbh='9151010609614944X4';
--中介人员信息
select a.rowid,a.* from zjcs_user a where a.agencyguid='d58ca612-6133-f00a-8c51-83bde00a4546';
--中介受理明细表
select a.rowid,a.* from t_dchy_zjslmx a where a.zjid='d58ca612-6133-f00a-8c51-83bde00a4546';
--中介审核附件
select a.rowid,a.* from t_dchy_zjfj a where a.zjid='dcac7488-f133-f00a-9266-d5ca7b035c02'; 
--更新中介信息表，根据条件单条更新
--更新测绘单位信息
update zjcs_info  set rowguid=rowguid where yyzzbh='121000004507521118'

--测绘成果问题-Oracle
--预测
select a.rowid,a.* from t_dchy_chcgy a where a.ydchybh='Y2021071300201';
--实测
select a.rowid,a.* from t_dchy_chcg a where a.dchybh='2021072200100';
--测绘成果受理明细
select a.rowid,a.* from b_chcg_slmx a where a.cgid='0DA800B7789043E0B597E6F41F1DD3B7';
--业务信息  --取IID
select a.rowid,a.* from ut_dchy_scsh a where a.slmxid='C6A7E15C832947D4E053F203A8C05462';
--房产审核表
select * from t_dchy_chjlfg a where a.slmxid='C6A7E15C832947D4E053F203A8C05462';
--房产审核意见附件
select * from t_dchy_chjlfj a where a.htshid='C6E87D5A69090969E053F203A8C06DA0';
--佐证材料
select * from t_dchy_support_materials a where a.cgid = '0DA800B7789043E0B597E6F41F1DD3B7'
--文件名称规则
--AA_BB_CC_DD.7z
--委托信息
select * from t_dchy_xmsxzjht wt where wt.htid='8DDA03CDE5CF4CAC837D7FF57FE5DDDE';
select * from t_dchy_xmsxzjht wt where wt.htmc like '%成都大润%'
--受理结论
select * from t_dchy_shjl a where a.slmxid='C6A7E15C832947D4E053F203A8C05462';
--FTP
select * from st_server a;
--二维码
select * from t_dchy_qrcode a where a.dchybh='Y2021071300201';
select a.*,a.rowid from t_dchy_wsrw_hist a where dchybh = '2021061800200';
--二维码任务表
select a.*,a.rowid from  t_dchy_wsrw a where dchybh = '2021061800200';
--成果质检
select a.*,a.rowid from t_dchy_cgzj a where  a.dchybh = 'Y2021060400100';
select a.*,a.rowid from t_dchy_cgzj a where  a.state=1 and a.dchybh != '';
--并联验收信息没推送到多测合一
select * from t_dchy_cgrk a where a.dchybh = '2020073100300'
select * from t_dchy_cgrk a where a.rowguid = 'D6B22C6A6CCF4915AB541A472BB5697A'


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
     and a.yzguid = '2814f1bc-a881-493c-9ac6-432d63c8f095'


  select a.htid  as "wtid",                     
       a.htmc  as "wtmc",                       
       a.htje  as "wtje",                       
       a.xzq   as "xzqdm",                      
       b.xzqmc as "xzqmc",                      
       a.xmmc  as "xmmc",                       
       a.type  as "type"                        
  from t_dchy_xmsxzjht a, t_dchy_xzq b            
 where a.xzq = b.xzqdm                            
   and a.yzid = '2814f1bc-a881-493c-9ac6-432d63c8f095'                                
   and a.htmc like concat(concat('%', ''), '%')   
 order by a.edittime desc
