One liner if one a box with internal IP and want to quickly determine other up hosts in the range



    prefix=10.13.0; for i in `seq 1 254`; do ping -c 1 -W 1 $prefix.$i > /dev/null 2>&1 && echo "$prefix.$i is up"; done



