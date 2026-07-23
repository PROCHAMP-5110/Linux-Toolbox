#!/usr/bin/env python3
import gi
gi.require_version("Gtk", "3.0")
from gi.repository import Gtk, Gdk

import json
import os


class LinuxToolbox(Gtk.Window):

    def __init__(self):
        super().__init__(title="Linux Toolbox")
        self.set_default_size(1000, 700)
        self.set_border_width(15)

        # =====================================================
        # FAVORITES
        # =====================================================

        self.favorites_file = os.path.expanduser(
            "~/.linux_toolbox_favorites.json"
        )

        self.favorites = self.load_favorites()

        # =====================================================
        # COMMAND DATABASE
        #
        # Format:
        # Category
        # Command
        # Description
        # Safety Level
        # Example
        # =====================================================

        self.commands = [

            # =================================================
            # FILES & FOLDERS
            # =================================================

            (
                "Files & Folders",
                "ls",
                "List files and folders",
                "SAFE",
                "ls -la"
            ),

            (
                "Files & Folders",
                "pwd",
                "Show the current directory",
                "SAFE",
                "pwd"
            ),

            (
                "Files & Folders",
                "cd [folder]",
                "Change to another directory",
                "SAFE",
                "cd Documents"
            ),

            (
                "Files & Folders",
                "cd ..",
                "Move to the parent directory",
                "SAFE",
                "cd .."
            ),

            (
                "Files & Folders",
                "mkdir [folder]",
                "Create a new folder",
                "SAFE",
                "mkdir MyFolder"
            ),

            (
                "Files & Folders",
                "touch [file]",
                "Create a new empty file",
                "SAFE",
                "touch notes.txt"
            ),

            (
                "Files & Folders",
                "cp [source] [destination]",
                "Copy a file",
                "SAFE",
                "cp file.txt backup.txt"
            ),

            (
                "Files & Folders",
                "cp -r [folder] [destination]",
                "Copy a folder and its contents",
                "CAUTION",
                "cp -r MyFolder Backup"
            ),

            (
                "Files & Folders",
                "mv [source] [destination]",
                "Move or rename a file",
                "CAUTION",
                "mv old.txt new.txt"
            ),

            (
                "Files & Folders",
                "rm [file]",
                "Delete a file",
                "CAUTION",
                "rm old.txt"
            ),

            (
                "Files & Folders",
                "rm -r [folder]",
                "Delete a folder and its contents",
                "DANGEROUS",
                "rm -r MyFolder"
            ),

            (
                "Files & Folders",
                "rm -rf [folder]",
                "Forcefully delete a folder and its contents",
                "DANGEROUS",
                "rm -rf MyFolder"
            ),

            (
                "Files & Folders",
                "find . -name [name]",
                "Search for files or folders",
                "SAFE",
                "find . -name '*.txt'"
            ),

            (
                "Files & Folders",
                "tree",
                "Show files and folders as a tree",
                "SAFE",
                "tree"
            ),

            (
                "Files & Folders",
                "file [file]",
                "Show the type of a file",
                "SAFE",
                "file image.png"
            ),

            # =================================================
            # DISK & STORAGE
            # =================================================

            (
                "Disk & Storage",
                "df -h",
                "Show available disk space",
                "SAFE",
                "df -h"
            ),

            (
                "Disk & Storage",
                "du -sh [folder]",
                "Show the size of a folder",
                "SAFE",
                "du -sh Downloads"
            ),

            (
                "Disk & Storage",
                "lsblk",
                "List storage devices and partitions",
                "SAFE",
                "lsblk"
            ),

            (
                "Disk & Storage",
                "sudo fdisk -l",
                "List disk partitions",
                "CAUTION",
                "sudo fdisk -l"
            ),

            (
                "Disk & Storage",
                "sudo fdisk [device]",
                "Edit disk partition tables",
                "DANGEROUS",
                "sudo fdisk /dev/sda"
            ),

            (
                "Disk & Storage",
                "mount [device] [folder]",
                "Mount a filesystem",
                "CAUTION",
                "sudo mount /dev/sdb1 /mnt"
            ),

            (
                "Disk & Storage",
                "umount [folder]",
                "Unmount a filesystem",
                "CAUTION",
                "sudo umount /mnt"
            ),

            (
                "Disk & Storage",
                "sudo mkfs [device]",
                "Create a filesystem on a device",
                "DANGEROUS",
                "sudo mkfs /dev/sdb1"
            ),

            # =================================================
            # SYSTEM INFORMATION
            # =================================================

            (
                "System Information",
                "uname -a",
                "Show detailed kernel information",
                "SAFE",
                "uname -a"
            ),

            (
                "System Information",
                "hostname",
                "Show the computer hostname",
                "SAFE",
                "hostname"
            ),

            (
                "System Information",
                "whoami",
                "Show the current username",
                "SAFE",
                "whoami"
            ),

            (
                "System Information",
                "uptime",
                "Show how long the system has been running",
                "SAFE",
                "uptime"
            ),

            (
                "System Information",
                "free -h",
                "Show RAM and swap usage",
                "SAFE",
                "free -h"
            ),

            (
                "System Information",
                "lscpu",
                "Show CPU information",
                "SAFE",
                "lscpu"
            ),

            (
                "System Information",
                "lsusb",
                "List connected USB devices",
                "SAFE",
                "lsusb"
            ),

            (
                "System Information",
                "lspci",
                "List PCI devices",
                "SAFE",
                "lspci"
            ),

            # =================================================
            # PACKAGES
            # =================================================

            (
                "Packages / APT",
                "sudo apt update",
                "Update package lists",
                "SAFE",
                "sudo apt update"
            ),

            (
                "Packages / APT",
                "sudo apt upgrade",
                "Upgrade installed packages",
                "CAUTION",
                "sudo apt upgrade"
            ),

            (
                "Packages / APT",
                "sudo apt install [package]",
                "Install a package",
                "CAUTION",
                "sudo apt install firefox"
            ),

            (
                "Packages / APT",
                "sudo apt remove [package]",
                "Remove a package",
                "CAUTION",
                "sudo apt remove firefox"
            ),

            (
                "Packages / APT",
                "sudo apt purge [package]",
                "Remove a package and its configuration",
                "CAUTION",
                "sudo apt purge firefox"
            ),

            (
                "Packages / APT",
                "sudo apt autoremove",
                "Remove unused packages",
                "CAUTION",
                "sudo apt autoremove"
            ),

            (
                "Packages / APT",
                "sudo apt search [package]",
                "Search for a package",
                "SAFE",
                "sudo apt search firefox"
            ),

            # =================================================
            # NETWORKING
            # =================================================

            (
                "Networking",
                "ip a",
                "Show network interfaces and IP addresses",
                "SAFE",
                "ip a"
            ),

            (
                "Networking",
                "ip route",
                "Show the network routing table",
                "SAFE",
                "ip route"
            ),

            (
                "Networking",
                "hostname -I",
                "Show local IP addresses",
                "SAFE",
                "hostname -I"
            ),

            (
                "Networking",
                "ping [address]",
                "Test a network connection",
                "SAFE",
                "ping google.com"
            ),

            (
                "Networking",
                "ss -tuln",
                "Show listening network ports",
                "SAFE",
                "ss -tuln"
            ),

            (
                "Networking",
                "curl [url]",
                "Request data from a URL",
                "CAUTION",
                "curl https://example.com"
            ),

            (
                "Networking",
                "wget [url]",
                "Download a file from the internet",
                "CAUTION",
                "wget https://example.com/file.zip"
            ),

            # =================================================
            # PROCESSES
            # =================================================

            (
                "Processes",
                "ps aux",
                "Show all running processes",
                "SAFE",
                "ps aux"
            ),

            (
                "Processes",
                "top",
                "Show a live process monitor",
                "SAFE",
                "top"
            ),

            (
                "Processes",
                "htop",
                "Show an interactive process monitor",
                "SAFE",
                "htop"
            ),

            (
                "Processes",
                "kill [PID]",
                "Stop a process",
                "CAUTION",
                "kill 1234"
            ),

            (
                "Processes",
                "kill -9 [PID]",
                "Forcefully stop a process",
                "DANGEROUS",
                "kill -9 1234"
            ),

            (
                "Processes",
                "pkill [name]",
                "Stop processes by name",
                "CAUTION",
                "pkill firefox"
            ),

            # =================================================
            # USERS & GROUPS
            # =================================================

            (
                "Users & Groups",
                "users",
                "Show currently logged-in users",
                "SAFE",
                "users"
            ),

            (
                "Users & Groups",
                "whoami",
                "Show the current user",
                "SAFE",
                "whoami"
            ),

            (
                "Users & Groups",
                "groups",
                "Show groups of the current user",
                "SAFE",
                "groups"
            ),

            (
                "Users & Groups",
                "sudo adduser [username]",
                "Create a new user",
                "CAUTION",
                "sudo adduser john"
            ),

            (
                "Users & Groups",
                "sudo deluser [username]",
                "Delete a user",
                "DANGEROUS",
                "sudo deluser john"
            ),

            # =================================================
            # PERMISSIONS
            # =================================================

            (
                "Permissions",
                "ls -l",
                "Show file permissions and ownership",
                "SAFE",
                "ls -l"
            ),

            (
                "Permissions",
                "chmod +x [file]",
                "Make a file executable",
                "CAUTION",
                "chmod +x script.sh"
            ),

            (
                "Permissions",
                "chmod 755 [file]",
                "Set common executable permissions",
                "CAUTION",
                "chmod 755 script.sh"
            ),

            (
                "Permissions",
                "chown [user] [file]",
                "Change file ownership",
                "CAUTION",
                "sudo chown john file.txt"
            ),

            (
                "Permissions",
                "sudo [command]",
                "Run a command with administrator privileges",
                "CAUTION",
                "sudo apt update"
            ),

            # =================================================
            # SYSTEMD
            # =================================================

            (
                "Systemd",
                "systemctl status [service]",
                "Show service status",
                "SAFE",
                "systemctl status bluetooth"
            ),

            (
                "Systemd",
                "sudo systemctl start [service]",
                "Start a service",
                "CAUTION",
                "sudo systemctl start bluetooth"
            ),

            (
                "Systemd",
                "sudo systemctl stop [service]",
                "Stop a service",
                "CAUTION",
                "sudo systemctl stop bluetooth"
            ),

            (
                "Systemd",
                "sudo systemctl restart [service]",
                "Restart a service",
                "CAUTION",
                "sudo systemctl restart bluetooth"
            ),

            (
                "Systemd",
                "sudo systemctl enable [service]",
                "Enable a service at startup",
                "CAUTION",
                "sudo systemctl enable bluetooth"
            ),

            (
                "Systemd",
                "sudo systemctl disable [service]",
                "Disable a service at startup",
                "CAUTION",
                "sudo systemctl disable bluetooth"
            ),

            # =================================================
            # GIT
            # =================================================

            (
                "Git",
                "git init",
                "Create a new Git repository",
                "SAFE",
                "git init"
            ),

            (
                "Git",
                "git clone [url]",
                "Clone a Git repository",
                "SAFE",
                "git clone https://github.com/user/project.git"
            ),

            (
                "Git",
                "git status",
                "Show the current Git status",
                "SAFE",
                "git status"
            ),

            (
                "Git",
                "git add .",
                "Stage changed files",
                "CAUTION",
                "git add ."
            ),

            (
                "Git",
                "git commit -m \"message\"",
                "Create a Git commit",
                "SAFE",
                "git commit -m \"Initial commit\""
            ),

            (
                "Git",
                "git push",
                "Push commits to a remote repository",
                "CAUTION",
                "git push"
            ),

            (
                "Git",
                "git pull",
                "Download and merge remote changes",
                "CAUTION",
                "git pull"
            ),

            (
                "Git",
                "git reset --hard",
                "Discard local changes",
                "DANGEROUS",
                "git reset --hard"
            ),

            # =================================================
            # HELP
            # =================================================

            (
                "Help",
                "man [command]",
                "Open the manual page for a command",
                "SAFE",
                "man ls"
            ),

            (
                "Help",
                "[command] --help",
                "Show help information",
                "SAFE",
                "ls --help"
            ),

            (
                "Help",
                "which [command]",
                "Show the location of a command",
                "SAFE",
                "which python3"
            ),

            (
                "Help",
                "history",
                "Show previously used commands",
                "SAFE",
                "history"
            ),

            (
                "Help",
                "clear",
                "Clear the terminal screen",
                "SAFE",
                "clear"
            ),
        ]

        # =====================================================
        # MAIN LAYOUT
        # =====================================================

        main_box = Gtk.Box(
            orientation=Gtk.Orientation.VERTICAL,
            spacing=10
        )

        self.add(main_box)

        # TITLE
        title = Gtk.Label()

        title.set_markup(
            "<big><b>🐧 Linux Toolbox</b></big>"
        )

        main_box.pack_start(
            title,
            False,
            False,
            5
        )

        subtitle = Gtk.Label(
            label="Your Linux command reference"
        )

        main_box.pack_start(
            subtitle,
            False,
            False,
            0
        )

        # SEARCH
        self.search = Gtk.SearchEntry()

        self.search.set_placeholder_text(
            "🔍 Search commands..."
        )

        self.search.connect(
            "search-changed",
            self.filter_commands
        )

        main_box.pack_start(
            self.search,
            False,
            False,
            5
        )

        # CATEGORY
        self.category = Gtk.ComboBoxText()

        self.category.append_text(
            "All Categories"
        )

        categories = sorted(
            set(
                command[0]
                for command in self.commands
            )
        )

        for category in categories:

            self.category.append_text(
                category
            )

        self.category.append_text(
            "⭐ Favorites"
        )

        self.category.set_active(
            0
        )

        self.category.connect(
            "changed",
            self.filter_commands
        )

        main_box.pack_start(
            self.category,
            False,
            False,
            5
        )

        # FAVORITE COUNT
        self.favorite_label = Gtk.Label()

        main_box.pack_start(
            self.favorite_label,
            False,
            False,
            0
        )

        # SCROLL AREA
        self.scroll = Gtk.ScrolledWindow()

        self.scroll.set_policy(
            Gtk.PolicyType.AUTOMATIC,
            Gtk.PolicyType.AUTOMATIC
        )

        self.list_box = Gtk.ListBox()

        self.list_box.set_selection_mode(
            Gtk.SelectionMode.NONE
        )

        self.scroll.add(
            self.list_box
        )

        main_box.pack_start(
            self.scroll,
            True,
            True,
            5
        )

        self.display_commands(
            self.commands
        )

    # =====================================================
    # FAVORITES
    # =====================================================

    def load_favorites(self):

        try:

            with open(
                self.favorites_file,
                "r"
            ) as file:

                return set(
                    json.load(file)
                )

        except:

            return set()

    def save_favorites(self):

        with open(
            self.favorites_file,
            "w"
        ) as file:

            json.dump(
                list(self.favorites),
                file
            )

    def toggle_favorite(
        self,
        button,
        command
    ):

        if command in self.favorites:

            self.favorites.remove(
                command
            )

        else:

            self.favorites.add(
                command
            )

        self.save_favorites()

        self.filter_commands(
            None
        )

    # =====================================================
    # DISPLAY COMMANDS
    # =====================================================

    def display_commands(
        self,
        commands
    ):

        for child in self.list_box.get_children():

            self.list_box.remove(
                child
            )

        for (
            category,
            command,
            description,
            safety,
            example
        ) in commands:

            row = Gtk.ListBoxRow()

            outer_box = Gtk.Box(
                orientation=Gtk.Orientation.VERTICAL,
                spacing=6
            )

            outer_box.set_border_width(
                12
            )

            # CATEGORY
            category_label = Gtk.Label()

            category_label.set_markup(
                f"<small><b>{category}</b></small>"
            )

            category_label.set_xalign(
                0
            )

            # COMMAND
            command_label = Gtk.Label()

            command_label.set_markup(
                f"<b>{command}</b>"
            )

            command_label.set_xalign(
                0
            )

            # DESCRIPTION
            description_label = Gtk.Label(
                label=description
            )

            description_label.set_xalign(
                0
            )

            # SAFETY
            if safety == "SAFE":

                safety_text = "🟢 SAFE"

            elif safety == "CAUTION":

                safety_text = "🟡 CAUTION"

            else:

                safety_text = "🔴 DANGEROUS"

            safety_label = Gtk.Label()

            safety_label.set_markup(
                f"<b>{safety_text}</b>"
            )

            safety_label.set_xalign(
                0
            )

            # EXAMPLE
            example_label = Gtk.Label()

            example_label.set_markup(
                f"<small>Example: <b>{example}</b></small>"
            )

            example_label.set_xalign(
                0
            )

            # BUTTONS
            button_box = Gtk.Box(
                orientation=Gtk.Orientation.HORIZONTAL,
                spacing=5
            )

            copy_button = Gtk.Button(
                label="📋 Copy"
            )

            copy_button.connect(
                "clicked",
                self.copy_command,
                command,
                safety
            )

            if command in self.favorites:

                favorite_button = Gtk.Button(
                    label="⭐ Remove Favorite"
                )

            else:

                favorite_button = Gtk.Button(
                    label="☆ Add Favorite"
                )

            favorite_button.connect(
                "clicked",
                self.toggle_favorite,
                command
            )

            button_box.pack_start(
                copy_button,
                False,
                False,
                0
            )

            button_box.pack_start(
                favorite_button,
                False,
                False,
                0
            )

            # ADD EVERYTHING
            outer_box.pack_start(
                category_label,
                False,
                False,
                0
            )

            outer_box.pack_start(
                command_label,
                False,
                False,
                0
            )

            outer_box.pack_start(
                description_label,
                False,
                False,
                0
            )

            outer_box.pack_start(
                safety_label,
                False,
                False,
                0
            )

            outer_box.pack_start(
                example_label,
                False,
                False,
                0
            )

            outer_box.pack_start(
                button_box,
                False,
                False,
                5
            )

            row.add(
                outer_box
            )

            self.list_box.add(
                row
            )

        self.favorite_label.set_text(
            f"⭐ Favorites: {len(self.favorites)}"
        )

        self.list_box.show_all()

    # =====================================================
    # SEARCH & FILTER
    # =====================================================

    def filter_commands(
        self,
        widget
    ):

        search_text = (
            self.search
            .get_text()
            .lower()
        )

        selected_category = (
            self.category
            .get_active_text()
        )

        filtered = []

        for (
            category,
            command,
            description,
            safety,
            example
        ) in self.commands:

            search_matches = (

                search_text in
                command.lower()

                or

                search_text in
                description.lower()

                or

                search_text in
                category.lower()

            )

            if selected_category == "⭐ Favorites":

                category_matches = (
                    command in self.favorites
                )

            else:

                category_matches = (

                    selected_category
                    == "All Categories"

                    or

                    selected_category
                    == category

                )

            if (
                search_matches
                and
                category_matches
            ):

                filtered.append(
                    (
                        category,
                        command,
                        description,
                        safety,
                        example
                    )
                )

        self.display_commands(
            filtered
        )

    # =====================================================
    # COPY COMMAND + WARNING
    # =====================================================

    def copy_command(
        self,
        button,
        command,
        safety
    ):

        if safety == "DANGEROUS":

            dialog = Gtk.MessageDialog(
                parent=self,
                flags=0,
                message_type=Gtk.MessageType.WARNING,
                buttons=Gtk.ButtonsType.OK_CANCEL,
                text="⚠️ Dangerous Command"
            )

            dialog.format_secondary_text(
                "This command can cause serious damage "
                "or data loss if used incorrectly.\n\n"
                f"Command:\n{command}\n\n"
                "Are you sure you want to copy it?"
            )

            response = dialog.run()

            dialog.destroy()

            if response != Gtk.ResponseType.OK:

                return

        clipboard = Gtk.Clipboard.get(
            Gdk.SELECTION_CLIPBOARD
        )

        clipboard.set_text(
            command,
            -1
        )

        clipboard.store()


# =========================================================
# START APPLICATION
# =========================================================

window = LinuxToolbox()

window.connect(
    "destroy",
    Gtk.main_quit
)

window.show_all()

Gtk.main()
