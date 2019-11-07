<!--
title: NanoStat
layout: IndexLayout
visible: true
-->

<style>
body, html { background: #fff; }
.markdown{ padding: 0 20px; }
.jumbotron {
  position: absolute;
  background-color: #383838;
  top: 56px;
  left: 0;
  right: 0;
  padding-top: 80px;
  min-height: 380px;
  color: #c1c1c1;
}
.jumbotron-block { min-height: 400px; }
.jumbotron-warpper {
  max-width: 1200px;
  padding: 0 30px;
  margin: 0 auto;
}
.jumbotron-title {
  font-size: 30px;
  font-weight: bold;
  padding-bottom: 20px;
}
.jumbotron-des {
  font-size: 1.25rem;
  line-height: 1.5;
  font-weight: 300;
  margin-bottom: 30px;
  font-family: -apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol";
}
.jumbotron .jumbotron-btn {
  display: inline-block;
  color: #333;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  user-select: none;
  background-color: #fff;
  padding: .375rem .75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: .25rem;
  transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
}
.jumbotron-btn:hover {
  background-color: #bbb;
  color: #333;
}
.jumbotron-btn:focus {
  outline: 0;
  box-shadow: 0 0 0 0.2rem rgba(255, 255, 255, 0.25);
}
</style>
<div class="jumbotron">
  <div class="jumbotron-warpper">
    <div class="jumbotron-title">NanoStat </div>
    <div class="jumbotron-des">NanoStat is an part of open source APM (Application Performance Management) solution. The core value of NanoStat is troubleshooting app issues and giving more visibility into performance bottlenecks.<br/> <br/>
  </div>
</div>
<div class="jumbotron-block"> </div>

### Using Scenarios

- Identify the responsibilities between maintaince and application development team
- Large-scale application changing management
- Profiling application database accessing Behavor

### Why NanoStat

- Open source and free
- Deploy without performance penalty and risks by traffic mirroring
- Support all popular relational databases includes: MySQL, PostgreSQL, Oracle, SQL Server, DB2
- Great performance based on PF_RING which support large databases instances

### Core Concepts

`SQL Pattern` is an result of generalization SQL by removing the constant inside SQL, includes: string, integer, hex, list. For example:
```sql
/* Original SQL */
SELECT no_o_id FROM new_order WHERE no_d_id = 3 AND no_w_id = 5 ORDER BY no_o_id ASC;

/* SQL Pattern */
SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC;
```

### Command

```shell
Usage: nanostat [options]

Generate application database access behaviors reports based on sql patterns.

Options:

	-d --database        database, example: mysql
	
	-n --number          top limit, default: 10, max value is: 1000
	
	-i --interval        interval, example: 60m, 24h, 7d, 4w, 12M, 100y, default is 60m
	
	
	
	-c --content         contents, example: type, keyword, frequent, return, time, all, default is all
	
    -t --type            output type, example: pdf, default: terminal

Examples:

  $ nanostat mysql       # equal to: nanostat -d mysql -n 10 -i 60m -c all
```

### Example Output

```shell
output duration: 2019-11-05 19:00~19:02

interval:19:00~19:01
	type:
	
		ddl:    0(0)
		dml:    3(3)
		dql:    19(19)
		dcl:    0(0)
		tcl:    6(6)
	
	keyword:
		
		insert: 3
		delete: 0
		update: 0
		select: 19
		table:  0
		database:   0
		index:  0
		synonym:    0
		
	frequent:

		rank:1	frequent:100
		pattern: "SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC"		
		rank:2	frequent:80
		pattern: "SELECT c_discount, c_last, c_credit, w_tax  FROM customer, warehouse WHERE w_id =? AND w_id = c_w_id AND c_d_id =? AND c_id =?"

	time:

		rank:1	response:5.010(1.080,15.210)
		pattern: "SELECT c_discount, c_last, c_credit, w_tax  FROM customer, warehouse WHERE w_id =? AND w_id = c_w_id AND c_d_id =? AND c_id =?"
		rank:2	response:3.010(1.100,5.210)
		pattern: "SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC"		
		
	return:
	
		rank:1	rows:100(1,199)
		pattern: "SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC"		
		rank:2	rows:10(1,19)
		pattern: "SELECT c_discount, c_last, c_credit, w_tax  FROM customer, warehouse WHERE w_id =? AND w_id = c_w_id AND c_d_id =? AND c_id =?"
		
interval:19:01~19:02
	type:
	
		ddl:	0(0)
		dml:    3(3)
		dql:	19(19)
		dcl:	0(0)
		tcl:	6(6)
	
	keyword:
		
		insert: 3
		delete: 0
		update: 0
		select: 19
		table:  0
		database:   0
		index:  0
		synonym:    0
		
	frequent:

		rank:1	frequent:100
		pattern: "SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC"		
		rank:2	frequent:80
		pattern: "SELECT c_discount, c_last, c_credit, w_tax  FROM customer, warehouse WHERE w_id =? AND w_id = c_w_id AND c_d_id =? AND c_id =?"

	time:

		rank:1	response:5.010(1.080,15.210)
		pattern: "SELECT c_discount, c_last, c_credit, w_tax  FROM customer, warehouse WHERE w_id =? AND w_id = c_w_id AND c_d_id =? AND c_id =?"
		rank:2	response:3.010(1.100,5.210)
		pattern: "SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC"		
		
	return:
	
		rank:1	rows:100(1,199)
		pattern: "SELECT no_o_id FROM new_order WHERE no_d_id = ? AND no_w_id = ? ORDER BY no_o_id ASC"		
		rank:2	rows:10(1,19)
		pattern: "SELECT c_discount, c_last, c_credit, w_tax  FROM customer, warehouse WHERE w_id =? AND w_id = c_w_id AND c_d_id =? AND c_id =?"
		
```

NOTE: Command input time is: 2019-11-05 19:02

### Contact Us

For alpha test or commercial cooperation, contact us by smartbin_zhang#163.com
