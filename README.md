TASK DATE: 23.11.2017 - Finished: 23.11.2017 (EASY)

TASK SHORT DESCRIPTION: 462/463 (searching NULL dobs/ages in advanced filters)

GITHUB REPOSITORY CODE: hotfix/task-462_463-filtering-null-values-on-dob-and-age

ORIGINAL WORK: https://github.com/BusinessBecause/network-site/tree/hotfix/task-462_463-filtering-null-values-on-dob-and-age

CHANGES
 
	IN FILES: 
	
		C:\toucantech.dev\network-site\addons\default\modules\bbusers\models\user_query_m.php
		
			CHANGED CODE at two places inside function _subquery_offline_where_cond and function _subquery_where_cond 
			
			FROM: $cond = '(' . $this->profile_table.'.dob_offline='.$dob . ')';
			
			TO: 
			
				if ($dob == '') {
					$cond = '(' . $this->profile_table.'.dob_offline = NULL or ' . $this->profile_table.'.dob_offline = 0)';
				} 
				else {
					$cond = '(' . $this->profile_table.'.dob_offline='.$dob . ')';
				}
