#!/bin/bash
# Bash script by Kartojal.

# Principal menu 
dcct_menu() {
 choice=`zenity --width=300 --height=250 --list --column="Select an action" --title="dcct-gui"  \
           "Plot Burst" \
           "Mine Burst" \
           "Optimize plots" \
           "About"`

 case "${choice}" in 
    "Plot Burst" )
        choice=""
        cpu_plot
        plot_burst
        ;;
    "Mine Burst" )
        choice=""
        mine_burst
        ;;
    "Optimize plots" )
        choice=""
        optimize_plot
        ;;
    "About")
        choice=""
        about
        ;;
     *)
        choice=""
        exit
         ;;
 esac

}

cpu_plot(){
    CPU_CHOICE=`zenity --width=300 --height=250 --list --column="Select an action" --title="dcct-gui"  \
               "SSE4 (Recommended)" \
               "AVX2 (Haswell & Bulldozer CPUs)" \
               "Default (Slower but support all CPU)" `

    case "${CPU_CHOICE}" in
       "SSE4 (Recommended)" )
            CPU_CODE="1"
            return
            ;;
       "AVX2 (Haswell & Bulldozer CPUs)" )
            CPU_CODE="2"
            return
            ;;
        "Default (Slower but support all CPU)" )
            CPU_CODE="0"
            return
            ;;
         *)
             dcct_menu
             ;;
     esac
      

}
# Mine Burst section
# First, ask the user the pool IP
mine_burst() {
    POOL=`zenity --forms  --title="dcct-gui ~ Mine Burst" --text="Insert the pool IP" --add-entry="Pool IP" `
    case $? in
    0)
        zenity --question --text="Pool IP is ${POOL}. Are you sure? If yes, press \"OK\"." 
        case $? in
            0)
                mine_plot_dir
                ;;
            1)
                mine_burst
                ;;
           -1)
                unknown_error
                ;;
        esac   
        ;;
    1)
        dcct_menu
        ;;
    -1)
        unknown_error
        ;;
    esac

}

# Ask the users the plots directory/ies.
mine_plot_dir(){
    zenity --info --width=380 --height=90 --text="Now press \"OK\" to select your Plot directory, also you can press CONTROL key to select multiple directories, if you want." 
    case $? in
        0)
            IFS=$'\n' FILE=($(zenity --file-selection --width=100 --height=100 --directory --multiple --separator=$'\n' --title="Select the plot directory"))
            case $? in
            0)
                mine_previous
                ;;
            1)
                mine_burst
                ;;
            -1)
                unknown_eror
                ;;
            esac
            ;;
        1)
            mine_burst
            ;;
       -1)
            unknown_error
            ;;
    esac
            
}
about(){
    README="./README.md"
    zenity --text-info --filename=${README}
    case $? in
        *)
            dcct_menu
            ;;
    esac
}
# Unknown error.
unknown_error(){
    zenity --error --text="Unknown error, ask for support in http://www.burstforum.com"
    exit 1
}
# Previous to mine, see all the info and ask if the user want to continue
mine_previous() {
    zenity --question --text="The selected Pool IP is ${POOL}. \n The plots directory are: \n `echo ${FILE} | sed -e 's \; \\n g' ` \n ¿Do you want start mining NOW?" 
    case $? in
        0)
            mine_pool_now
            ;;
        1)
            mine_burst
            ;;
        -1)
            unknown_eror
            ;;
    esac


}

# Open a terminal, launch the dcct miner with the arguments
mine_pool_now() {
    lxterm -hold -e dcct-mine "${POOL}" "${FILE[@]}"
  # "`echo ${FILE} | sed -e 's:\;: :g' | sed -e 's: :\" \":g' `"

}
# GUI CPU PLOTTER section
plot_burst() {
    PLOT_FORM=`zenity  --forms --title="DCCT Plotter GUI" --text="Enter the following values" --separator="," --add-entry="BURST ID" --add-entry="Start nonce" --add-entry="Plot size in GBytes" --add-entry="RAM Memory to plot (MBytes)" --add-entry="CPU Threads"`
    case $? in
        0)
            BURST_ID=$(awk -F, '{print $1}' <<<$PLOT_FORM)
            START_NONCE=$(awk -F, '{print $2}' <<<$PLOT_FORM)
            PLOT_SIZE=$(awk -F, '{print $3}' <<<$PLOT_FORM)
            PLOT_SIZE_NONCES=$(( $PLOT_SIZE * 1024 * 1024 / 256 ))
            STAGGER_SIZE=$(awk -F, '{print $4}' <<<$PLOT_FORM)
            STAGGER_SIZE_NONCES=$(( $STAGGER_SIZE * 4 ))
            THREADS=$(awk -F, '{print $5}' <<<$PLOT_FORM)
            plot_burst_dir
            ;;
        1)
            dcct_menu 
            ;;
        -1)
            unknown_eror
            ;;
    esac
}
plot_burst_dir() {
  zenity --info --text="Now press \"OK\" to select the directory  to save your Plots." 
    case $? in
        0)
            PLOT_DIR=`zenity --file-selection --directory --title="Select the plot directory"`
            case $? in
            0)
                plot_previous
                ;;
            1)
                plot_burst
                ;;
            -1)
                unknown_eror
                ;;
            esac
            ;;
        1)
            plot_burst
            ;;
       -1)
            unknown_error
            ;;
    esac

}
plot_previous() {
    zenity --question --text="Plot Info \n\n BURST-ID: ${BURST_ID} \n Start nonce: ${START_NONCE}\n Plot size: ${PLOT_SIZE} GB \( ${PLOT_SIZE_NONCES} nonces \) \n Stagger: ${STAGGER_SIZE} MB \( ${STAGGER_SIZE_NONCES} nonces \) \n CPU threads: ${THREADS} \n ¿Do you want to continue and start plotting?" 
    case $? in
        0)
            start_plotting
            ;;
        1)
            plot_burst
            ;;
        -1)
            unknown_eror
            ;;
         *)
             exit 0
             ;;
    esac



}
start_plotting(){
    # Thanks to Mirkic7 for MDCCT version with AVX2 and SSE4 support
    if [ $CPU_CODE > 0 ] ;then
        lxterm -hold -e ./plotavx2 -x ${CPU_CODE} -k ${BURST_ID} -d ${PLOT_DIR} -s ${START_NONCE} -n ${PLOT_SIZE_NONCES} -m ${STAGGER_SIZE_NONCES} -t ${THREADS}

    else
        lxterm -hold -e ./plot -k ${BURST_ID} -d ${PLOT_DIR} -s ${START_NONCE} -n ${PLOT_SIZE_NONCES} -m ${STAGGER_SIZE_NONCES} -t ${THREADS}
        
    fi
}

optimize_plot(){
    `zenity  --question --title="DCCT Optimizer GUI" --text="Select the plot file to optimize it."`
 case $? in
        0)
            FILE=`zenity --file-selection --width=100 --height=100  --title="Select the plot file to optimize it."` 
            case $? in
                0)
                    lxterm -hold -e ./optimize ${FILE}
                    ;;
                1)
                    optimize_plot
                    ;;
                -1)
                    unknown_error
                    ;;
                 *)
                     echo "quepaso"
                     ;;

            esac
            ;;
        1)
            dcct_menu
            ;;
        -1)
            unknown_error
            ;;
         *)
             exit 0
             ;;
    esac

}
dcct_menu
