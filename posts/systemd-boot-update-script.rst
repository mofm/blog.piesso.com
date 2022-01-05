.. title: systemd-boot update script
.. slug: systemd-boot-update-script
.. date: 2021-12-19 04:23:45 UTC+03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

systemd-boot does not automatically regenerate entry configuration files like update-grup or grub-mkconfig. So you can use below script for Gentoo Linux.


.. code-block:: bash


        #!/bin/bash
        #
        # This is a simple kernel hook to populate the systemd-boot entries
        # whenever kernels are added or removed.
        #

        # The UUID of your disk.
        # Note: if using LVM, this should be the LVM partition.
        UUID="CHANGEME"

        # Intel microcode file name
        MCODE="CHANGEME"

        # Any rootflags you wish to set. For example, mine are currently
        # "subvol=@ quiet splash intel_pstate=enable".
        ROOTFLAGS="CHANGEME"

        # Our kernels.
        KERNELS=()
        FIND="find /boot -maxdepth 1 -name 'vmlinuz-*' -type f -not -name '*.old' -print0 | sort -Vrz"
        while IFS= read -r -u3 -d $'\0' LINE; do
                KERNEL=$(basename "${LINE}")
                KERNELS+=("${KERNEL:8}")
        done 3< <(eval "${FIND}")

        # There has to be at least one kernel.
        if [ ${#KERNELS[@]} -lt 1 ]; then
                echo -e "\e[2msystemd-boot\e[0m \e[1;31mNo kernels found.\e[0m"
                exit 1
        fi

        # Copy the latest kernel files to a consistent place so we can
        # keep using the same loader configuration.
        LATEST="${KERNELS[@]:0:1}"
        echo -e "\e[2msystemd-boot\e[0m \e[1;32m${LATEST}\e[0m"
        cat << EOF > /boot/loader/entries/gentoo.conf
        title   Gentoo Linux
        linux   /vmlinuz-${LATEST}
        initrd  /${MCODE}
        initrd  /initramfs-${LATEST}.img
        options root=UUID=${UUID} rw ${ROOTFLAGS}
        EOF
        #done

        # Copy any legacy kernels over too, but maintain their version-
        # based names to avoid collisions.
        if [ ${#KERNELS[@]} -gt 1 ]; then
                LEGACY=("${KERNELS[@]:1}")
                for VERSION in "${LEGACY[@]}"; do
                    echo -e "\e[2msystemd-boot\e[0m \e[1;32m${VERSION}\e[0m"
                    cat << EOF > /boot/loader/entries/gentoo-${VERSION}.conf
        title   Gentoo Linux ${VERSION}
        linux   /vmlinuz-${VERSION}
        initrd  /${MCODE}
        initrd  /initramfs-${VERSION}.img
        options root=UUID=${UUID} rw ${ROOTFLAGS}
        EOF
                done
        fi

        printf "\n"
        printf "Updating systemd-boot firmware \n"
        bootctl update

        # Success!
        echo -e "\e[2m---\e[0m"
        exit 0



This script forked from `here <https://blobfolio.com/2018/replace-grub2-with-systemd-boot-on-ubuntu-18-04/>`_.
