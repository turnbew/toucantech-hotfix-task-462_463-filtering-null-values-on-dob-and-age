TASK DATE: 23.11.2017 - Finished: 23.11.2017 (EASY)

TASK SHORT DESCRIPTION: 462/463 (searching NULL dobs/ages in advanced filters)

GITHUB REPOSITORY CODE: hotfix/task-462_463-filtering-null-values-on-dob-and-age

ORIGINAL WORK: https://github.com/BusinessBecause/network-site/tree/hotfix/task-462_463-filtering-null-values-on-dob-and-age

CHANGES
 
	IN FILES: 
	
		\network-site\addons\default\modules\bbusers\models\user_query_m.php
		
		
			CHANGED CODE 1: inside function _subquery_where_cond 
			
				FROM: $cond = '(' . $this->profile_table.'.dob_offline='.$dob . ')';
				
				TO: 
				
					if ($dob == '') {
						$cond = '(' . $this->profile_table . '.dob is NULL )';
					} 
					else {
						$cond = '(' . $this->profile_table . '.dob = ' . $dob . ')';
					}
					
					
			CHANGED CODE 2 inside function _subquery_offline_where_cond
			
				FROM: $cond = '(' . $this->profile_table.'.dob_offline='.$dob . ')';
				
				TO: 
				
					if ($dob == '') {
						$cond = '(' . $this->profile_table . '.dob_offline is NULL )';
					} 
					else {
						$cond = '(' . $this->profile_table . '.dob_offline = ' . $dob . ')';
					}
					
					
			CHANGED CODE 3 - 4 : inside function _run_subquery 

				FROM:  $this->db->where('( ' . $sql . ') '); 
				
				TO:  $this->db->where('( ' . $sql . ') ', null, false);
				
				------------
				
				FROM:  $this->db->or_where('( ' . $offline_sql . ') ');
				
				TO:  $this->db->or_where('( ' . $offline_sql . ') ', null, false);
