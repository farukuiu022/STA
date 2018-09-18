# STA


set fr [open SUMM.rpt r]
while { [gets $fr setup_count] >=0} {
	if { [regexp "SETUP TIMING" $setup_count] } {
		for { set i 0 } { $i <= 10000} { incr i} {
		gets $fr setup_count1
			set lan_setup [llength [lappend count $i] ]
	if { [regexp "HOLD TIMING" $setup_count1] } {
					break 
				}
		}		
	}
}

set fr [open SUMM.rpt r]
while { [gets $fr setup1] >=0} {
	if { [regexp "SETUP TIMING" $setup1] } {
			set func_setup_sc_sum_fep 0;set func_setup_sc_swns 0;set func_setup_scR_sum_fep 0;set func_setup_scR_swns 0;set func_setup_sh_sum_fep 0;set func_setup_sh_swns 0
			set func_setup_shR_sfep 0;set func_setup_shR_swns 0;set mbist_setup_sc_sum_fep 0;set mbist_setup_sc_swns 0;set mbist_setup_scR_sum_fep 0;set mbist_setup_scR_swns 0
			set mbist_setup_sh_sum_fep 0;set mbist_setup_sh_swns 0;set mbist_setup_shR_sum_fep 0;set mbist_setup_shR_swns 0;set sc_setup_sc_sum_fep 0;set sc_setup_sc_swns 0
			set sc_setup_scR_sum_fep 0;set sc_setup_scR_swns 0;set sc_setup_sh_sum_fep 0;set sc_setup_sh_swns 0;set sc_setup_shR_sum_fep 0;set sc_setup_shR_swns 0
			set sca_setup_sc_sum_fep 0;set sca_setup_sc_swns 0;set sca_setup_scR_sum_fep 0;set sca_setup_scR_swns 0;set sca_setup_sh_sum_fep 0;set $sca_setup_sh_swns 0
			set sca_setup_shR_sum_fep 0;set sca_setup_shR_swns 0;set ss_setup_sc_sum_fep 0;set ss_setup_sc_swns 0;set ss_setup_scR_sum_fep 0;set ss_setup_scR_swns 0
			set ss_setup_sh_sum_fep 0;set ss_setup_sh_swns 0;set ss_setup_shR_sum_fep 0;set ss_setup_shR_swns 0
			for { set i 0 } { $i < $lan_setup} { incr i} {
			gets $fr setup2
			if { [regexp "func" $setup2] & [regexp "SC.SigCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				#puts $setup2
				set func_setup_sc_fep [lindex $setup2 3]
				set func_setup_sc_sum_fep [expr $func_setup_sc_sum_fep + $func_setup_sc_fep]
				
				lappend func_setup_sc_wns [lindex $setup2 4]
				set func_setup_sc_swns [lsort $func_setup_sc_wns]
				set func_setup_sc_swns [lindex $func_setup_sc_swns end]
			} else { if { $func_setup_sc_sum_fep > 0 } { set func_setup_sc_sum_fep $func_setup_sc_sum_fep;set func_setup_sc_swns $func_setup_sc_swns } else { set func_setup_sc_sum_fep 0;set func_setup_sc_swns 0 } }
			if { [regexp "func" $setup2] & [regexp "SC.SigRCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set func_setup_scR_fep [lindex $setup2 3]
				set func_setup_scR_sum_fep [expr $func_setup_scR_sum_fep + $func_setup_scR_fep]
				
				lappend func_setup_scR_wns [lindex $setup2 4]
				set func_setup_scR_swns [lsort $func_setup_scR_wns]	
				set func_setup_scR_swns [lindex $func_setup_scR_swns end]
			} else { if { $func_setup_scR_sum_fep > 0 } { set func_setup_scR_sum_fep $func_setup_scR_sum_fep;set func_setup_scR_swns $func_setup_scR_swns } else { set func_setup_scR_sum_fep 0;set func_setup_scR_swns 0 } }
			if { [regexp "func" $setup2] & [regexp "SH.SigCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set func_setup_sh_fep [lindex $setup2 3]
				set func_setup_sh_sum_fep [expr $func_setup_sh_sum_fep + $func_setup_sh_fep]
				
				lappend func_setup_sh_wns [lindex $setup2 4]
				set func_setup_sh_swns [lsort $func_setup_sh_wns]
				set func_setup_sh_swns [lindex $func_setup_sh_swns end]
			} else { if { $func_setup_sh_sum_fep > 0 } { set func_setup_sh_sum_fep $func_setup_sh_sum_fep;set func_setup_sh_swns $func_setup_sh_swns } else { set func_setup_sh_sum_fep 0;set func_setup_sh_swns 0 } }
			if { [regexp "func" $setup2] & [regexp "SH.SigRCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set func_setup_shR_fep [lindex $setup2 3]
				set func_setup_shR_sfep [expr $func_setup_shR_sfep + $func_setup_shR_fep]
				
				lappend func_setup_shR_wns [lindex $setup2 4]
				set func_setup_shR_swns [lsort $func_setup_shR_wns]
				set func_setup_shR_swns [lindex func_setup_shR_swns end]
			} else { if { $func_setup_shR_sfep > 0 } { set func_setup_shR_sfep $func_setup_shR_sfep;set func_setup_shR_swns $func_setup_shR_swns } else { set func_setup_shR_sfep 0;set func_setup_shR_swns 0 } }
			
			
			if { [regexp "mbist" $setup2] & [regexp "SC.SigCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set mbist_setup_sc_fep [lindex $setup2 3]
				set mbist_setup_sc_sum_fep [expr $mbist_setup_sc_sum_fep + $mbist_setup_sc_fep ]
				
				lappend mbist_setup_sc_wns [lindex $setup2 4]
				set mbist_setup_sc_swns [lsort $mbist_setup_sc_wns]
				set $mbist_setup_sc_swns [lindex $mbist_setup_sc_swns end]
			} else { if { $mbist_setup_sc_sum_fep > 0 } { set mbist_setup_sc_sum_fep $mbist_setup_sc_sum_fep;set mbist_setup_sc_swns $mbist_setup_sc_swns } else { set mbist_setup_sc_sum_fep 0;set mbist_setup_sc_swns 0 } }
			if { [regexp "mbist" $setup2] & [regexp "SC.SigRCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set mbist_setup_scR_fep [lindex $setup2 3]
				set mbist_setup_scR_sum_fep [expr $mbist_setup_scR_sum_fep + $mbist_setup_scR_fep]
				
				lappend mbist_setup_scR_wns [lindex $setup2 4]
				set mbist_setup_scR_swns [lsort $mbist_setup_scR_wns]
				set mbist_setup_scR_swns [lindex $mbist_setup_scR_swns end]
			} else { if { $mbist_setup_scR_sum_fep > 0 } { set mbist_setup_scR_sum_fep $mbist_setup_scR_sum_fep;set mbist_setup_scR_swns $mbist_setup_scR_swns } else { set mbist_setup_scR_sum_fep 0;set mbist_setup_scR_swns 0 } }
			if { [regexp "mbist" $setup2] & [regexp "SH.SigCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set mbist_setup_sh_fep [lindex $setup2 3]
				set mbist_setup_sh_sum_fep [expr $mbist_setup_sh_sum_fep + $mbist_setup_sh_fep]
				
				lappend mbist_setup_sh_wns [lindex $setup2 4]
				set mbist_setup_sh_swns [lsort $mbist_setup_sh_wns]
				set mbist_setup_sh_swns [lindex $mbist_setup_sh_swns end]
			} else { if { $mbist_setup_sh_sum_fep > 0 } { set mbist_setup_sh_sum_fep $mbist_setup_sh_sum_fep;set mbist_setup_sh_swns $mbist_setup_sh_swns } else { set mbist_setup_sh_sum_fep 0;set mbist_setup_sh_swns 0 } }
			if { [regexp "mbist" $setup2] & [regexp "SH.SigRCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set mbist_setup_shR_fep [lindex $setup2 3]
				set mbist_setup_shR_sum_fep [expr $mbist_setup_shR_sum_fep + $mbist_setup_shR_fep]
				
				lappend mbist_setup_shR_wns [lindex $setup2 4]
				set mbist_setup_shR_swns [lsort $mbist_setup_shR_wns]
				set mbist_setup_shR_swns [lindex $mbist_setup_shR_swns end]
			} else { if { $mbist_setup_shR_sum_fep > 0 } { set mbist_setup_shR_sum_fep $mbist_setup_shR_sum_fep;set mbist_setup_shR_swns $mbist_setup_shR_swns } else { set mbist_setup_shR_sum_fep 0;set mbist_setup_shR_swns 0 } }
			
			
			if { [regexp "sc" $setup2] & [regexp "SC.SigCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set sc_setup_sc_fep [lindex $setup2 3]
				set sc_setup_sc_sum_fep [expr $sc_setup_sc_sum_fep + $sc_setup_sc_fep]
				
				lappend sc_setup_sc_wns [lindex $setup2 4]
				set sc_setup_sc_swns [lsort $sc_setup_sc_wns]
				set sc_setup_sc_swns [lindex $sc_setup_sc_swns end]
			} else { if { $sc_setup_sc_sum_fep > 0 } { set sc_setup_sc_sum_fep $sc_setup_sc_sum_fep;set sc_setup_sc_swns $sc_setup_sc_swns } else { set sc_setup_sc_sum_fep 0;set sc_setup_sc_swns 0 } }
			if { [regexp "sc" $setup2] & [regexp "SC.SigRCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set sc_setup_scR_fep [lindex $setup2 3]
				set sc_setup_scR_sum_fep [expr $sc_setup_scR_sum_fep + $sc_setup_scR_fep]
				
				lappend sc_setup_scR_wns [lindex $setup2 4]
				set sc_setup_scR_swns [lsort $sc_setup_scR_wns]
				set sc_setup_scR_swns [lindex $sc_setup_scR_swns end]
			} else { if { $sc_setup_scR_sum_fep > 0 } { set sc_setup_scR_sum_fep $sc_setup_scR_sum_fep;set sc_setup_scR_swns $sc_setup_scR_swns } else { set sc_setup_scR_sum_fep 0;set sc_setup_scR_swns 0 } }
			if { [regexp "sc" $setup2] & [regexp "SH.SigCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set sc_setup_sh_fep [lindex $setup2 3]
				set sc_setup_sh_sum_fep [expr $sc_setup_sh_sum_fep + $sc_setup_sh_fep]
				
				lappend sc_setup_sh_wns [lindex $setup2 4]
				set sc_setup_sh_swns [lsort $sc_setup_sh_wns]
				set sc_setup_sh_swns [lindex $sc_setup_sh_swns end]
			} else { if { $sc_setup_sh_sum_fep > 0 } { set sc_setup_sh_sum_fep $sc_setup_sh_sum_fep;set sc_setup_sh_swns $sc_setup_sh_swns } else { set sc_setup_sh_sum_fep 0;set sc_setup_sh_swns 0 } }
			if { [regexp "sc" $setup2] & [regexp "SH.SigRCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set sc_setup_shR_fep [lindex $setup2 3]
				set sc_setup_shR_sum_fep [expr $sc_setup_shR_sum_fep + $sc_setup_shR_fep]
				
				lappend sc_setup_shR_wns [lindex $setup2 4]
				set sc_setup_shR_swns [lsort $sc_setup_shR_wns]
				set sc_setup_shR_swns [lindex $sc_setup_shR_swns end]
			} else { if { $sc_setup_shR_sum_fep > 0 } { set sc_setup_shR_sum_fep $sc_setup_shR_sum_fep;set sc_setup_shR_swns $sc_setup_shR_swns } else { set sc_setup_shR_sum_fep 0;set sc_setup_shR_swns 0 } }
			
			
			if { [regexp "sca" $setup2] & [regexp "SC.SigCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set sca_setup_sc_fep [lindex $setup2 3]
				set sca_setup_sc_sum_fep [expr $sca_setup_sc_sum_fep + $sca_setup_sc_fep]
				
				lappend sca_setup_sc_wns [lindex $setup2 4]
				set sca_setup_sc_swns [lsort $sca_setup_sc_wns]
				set sca_setup_sc_swns [lindex $sca_setup_sc_swns end]
			} else { if { $sca_setup_sc_sum_fep > 0 } { set sca_setup_sc_sum_fep $sca_setup_sc_sum_fep;set sca_setup_sc_swns $sca_setup_sc_swns } else { set sca_setup_sc_sum_fep 0;set sca_setup_sc_swns 0 } }
			if { [regexp "sca" $setup2] & [regexp "SC.SigRCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set sca_setup_scR_fep [lindex $setup2 3]
				set sca_setup_scR_sum_fep [expr $sca_setup_scR_sum_fep + $sca_setup_scR_fep]
				
				lappend sca_setup_scR_wns [lindex $setup2 4]
				set sca_setup_scR_swns [lsort $sca_setup_scR_wns]
				set sca_setup_scR_swns [lindex $sca_setup_scR_swns end]
			} else { if { $sca_setup_scR_sum_fep > 0 } { set sca_setup_scR_sum_fep $sca_setup_scR_sum_fep;set sca_setup_scR_swns $sca_setup_scR_swns } else { set sca_setup_scR_sum_fep 0;set sca_setup_scR_swns 0 } }
			if { [regexp "sca" $setup2] & [regexp "SH.SigCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set sca_setup_sh_fep [lindex $setup2 3]
				set sca_setup_sh_sum_fep [expr $sca_setup_sh_sum_fep + $sca_setup_sh_fep]
				
				lappend sca_setup_sh_wns [lindex $setup2 4]
				set sca_setup_sh_swns [lsort $sca_setup_sh_wns]
				set sca_setup_sh_swns [lindex $sca_setup_sh_swns end]
			} else { if { $sca_setup_sh_sum_fep > 0 } { set sca_setup_sh_sum_fep $sca_setup_sh_sum_fep;set sca_setup_sh_swns $sca_setup_sh_swns } else { set sca_setup_sh_sum_fep 0;set sca_setup_sh_swns 0 } }
			if { [regexp "sca" $setup2] & [regexp "SH.SigRCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set sca_setup_shR_fep [lindex $setup2 3]
				set sca_setup_shR_sum_fep [expr $sca_setup_shR_sum_fep + $sca_setup_shR_fep]
				
				lappend sca_setup_shR_wns [lindex $setup2 4]
				set sca_setup_shR_swns [lsort $sca_setup_shR_wns]
				set sca_setup_shR_swns [lindex $sca_setup_shR_swns end]
			} else { if { $sca_setup_shR_sum_fep > 0 } { set sca_setup_shR_sum_fep $sca_setup_shR_sum_fep;set sca_setup_shR_swns $sca_setup_shR_swns } else { set sca_setup_shR_sum_fep 0;set sca_setup_shR_swns 0 } }
			
			
			if { [regexp "ss" $setup2] & [regexp "SC.SigCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set ss_setup_sc_fep [lindex $setup2 3]
				set ss_setup_sc_sum_fep [expr $ss_setup_sc_sum_fep + $ss_setup_sc_fep]
				
				lappend ss_setup_sc_wns [lindex $setup2 4]
				set ss_setup_sc_swns [lsort $ss_setup_sc_wns]
				set ss_setup_sc_swns [lindex $ss_setup_sc_swns end]
			} else { if { $ss_setup_sc_sum_fep > 0 } { set ss_setup_sc_sum_fep $ss_setup_sc_sum_fep;set ss_setup_sc_swns $ss_setup_sc_swns } else { set ss_setup_sc_sum_fep 0;set ss_setup_sc_swns 0 } }
			if { [regexp "ss" $setup2] & [regexp "SC.SigRCmaxDP_ErPlus_modRvia_m40c" $setup2] } {
				set ss_setup_scR_fep [lindex $setup2 3]
				set ss_setup_scR_sum_fep [expr $ss_setup_scR_sum_fep + $ss_setup_scR_fep]
				
				lappend ss_setup_scR_wns [lindex $setup2 4]
				set ss_setup_scR_swns [lsort $ss_setup_scR_wns]
				set ss_setup_scR_swns [lindex $ss_setup_scR_swns end]
			} else { if { $ss_setup_scR_sum_fep > 0 } { set ss_setup_scR_sum_fep $ss_setup_scR_sum_fep;set ss_setup_scR_swns $ss_setup_scR_swns } else { set ss_setup_scR_sum_fep 0;set ss_setup_scR_swns 0 } }
			if { [regexp "ss" $setup2] & [regexp "SH.SigCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set ss_setup_sh_fep [lindex $setup2 3]
				set ss_setup_sh_sum_fep [expr $ss_setup_sh_sum_fep + $ss_setup_sh_fep]
				
				lappend ss_setup_sh_wns [lindex $setup2 4]
				set ss_setup_sh_swns [lsort $ss_setup_sh_wns]
				set ss_setup_sh_swns [lindex $ss_setup_sh_swns end]
			} else { if { $ss_setup_sh_sum_fep > 0 } { set ss_setup_sh_sum_fep $ss_setup_sh_sum_fep;set ss_setup_sh_swns $ss_setup_sh_swns } else { set ss_setup_sh_sum_fep 0;set ss_setup_sh_swns 0 } }
			if { [regexp "ss" $setup2] & [regexp "SH.SigRCmaxDP_ErPlus_modRvia_125c" $setup2] } {
				set ss_setup_shR_fep [lindex $setup2 3]
				set ss_setup_shR_sum_fep [expr $ss_setup_shR_sum_fep + $ss_setup_shR_fep]
				
				lappend ss_setup_shR_wns [lindex $setup2 4]
				set ss_setup_shR_swns [lsort $ss_setup_shR_wns]
				set ss_setup_shR_swns [lindex $ss_setup_shR_swns end]
			} else { if { $ss_setup_shR_sum_fep > 0 } { set ss_setup_shR_sum_fep $ss_setup_shR_sum_fep;set ss_setup_shR_swns $ss_setup_shR_swns } else { set ss_setup_shR_sum_fep 0;set ss_setup_shR_swns 0 } }
			
			
			if { [regexp "HOLD TIMING" $setup2] } {
					break 
			} 	
				
		}
	}
}
	puts "$func_setup_sc_sum_fep,$func_setup_sc_swns,$func_setup_scR_sum_fep,$func_setup_scR_swns,\
				$func_setup_sh_sum_fep,$func_setup_sh_swns,$func_setup_shR_sfep,$func_setup_shR_swns,\
			$mbist_setup_sc_sum_fep,$mbist_setup_sc_swns,$mbist_setup_scR_sum_fep,$mbist_setup_scR_swns,\
				$mbist_setup_sh_sum_fep,$mbist_setup_sh_swns,$mbist_setup_shR_sum_fep,$mbist_setup_shR_swns,\
			$sc_setup_sc_sum_fep,$sc_setup_sc_swns,$sc_setup_scR_sum_fep,$sc_setup_scR_swns,\
				$sc_setup_sh_sum_fep,$sc_setup_sh_swns,$sc_setup_shR_sum_fep,$sc_setup_shR_swns,\
			$sca_setup_sc_sum_fep,$sca_setup_sc_swns,$sca_setup_scR_sum_fep,$sca_setup_scR_swns,\
				$sca_setup_sh_sum_fep,$sca_setup_sh_swns,$sca_setup_shR_sum_fep,$sca_setup_shR_swns,\
			$ss_setup_sc_sum_fep,$ss_setup_sc_swns,$ss_setup_sh_sum_fep,$ss_setup_sh_swns,\
				$ss_setup_shR_sum_fep,$ss_setup_shR_swns"
