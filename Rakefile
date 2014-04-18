require 'pry'

# Install locally
INSTALL_PREFIX = "~/.icons"

# Theme folder name
THEME_NAME = "trollicons"

WD = Dir.pwd

CURSORS = "#{WD}/cursors"

SOURCE = "#{WD}/source"

X_COMPLIANT_CURSOR_NAMES = [
  "alias",
  "allscroll",
  "arrow",
  "based_arrow_down",
  "based_arrow_up",
  "bd_double_arrow",
  "bottom_left_corner",
  "bottom_right_corner",
  "bottom_side",
  "bottom_tee",
  "cell",
  "center_ptr",
  "circle",
  "clock",
  "closedhand",
  "colorpicker",
  "colresize",
  "contextmenu",
  "copy",
  "cross",
  "crossed_circle",
  "crosshair",
  "cross_reverse",
  "default",
  "diamond_cross",
  "dndask",
  "dndcopy",
  "dndlink",
  "dndmove",
  "dndno-drop",
  "dndnone",
  "dot",
  "dotbox",
  "double_arrow",
  "draft_large",
  "draft_small",
  "draped_box",
  "eresize",
  "ewresize",
  "fd_double_arrow",
  "fleur",
  "forbidden",
  "grabbing",
  "halfbusy",
  "hand",
  "hand1",
  "hand2",
  "h_double_arrow",
  "help",
  "ibeam",
  "icon",
  "iron_cross",
  "left_ptr",
  "left_ptr_watch",
  "left_side",
  "left_tee",
  "link",
  "ll_angle",
  "lr_angle",
  "move",
  "neresize",
  "neswresize",
  "nodrop",
  "notallowed",
  "nresize",
  "nsresize",
  "nwresize",
  "nwseresize",
  "openhand",
  "pencil",
  "pirate",
  "plus",
  "pointer",
  "pointing_hand",
  "progress",
  "question_arrow",
  "rightarrow",
  "right_ptr",
  "right_side",
  "right_tee",
  "rowresize",
  "sb_down_arrow",
  "sb_h_double_arrow",
  "sb_left_arrow",
  "sb_right_arrow",
  "sb_up_arrow",
  "sb_v_double_arrow",
  "seresize",
  "size_all",
  "size_bdiag",
  "size_fdiag",
  "size_hor",
  "size_ver",
  "sizing",
  "split_h",
  "split_v",
  "sresize",
  "swresize",
  "tcross",
  "text",
  "top_left_arrow",
  "top_left_corner",
  "top_right_corner",
  "top_side",
  "top_tee",
  "ul_angle",
  "up_arrow",
  "uparrow",
  "ur_angle",
  "v_double_arrow",
  "verticaltext",
  "wait",
  "watch",
  "whats_this",
  "wresize",
  "X_cursor",
  "Xcursor",
  "xterm",
  "zoomin",
  "zoom-out"
]

directory "cursors"
directory "source"

namespace :build do
  desc "Run necessary steps to produce a working cursor icon set"
  task :all => ["source", "cursors", "clean:all", "convert:all", "build:configure"] do
    Dir.chdir(SOURCE) do
      X_COMPLIANT_CURSOR_NAMES.each do |name|
        sh "xcursorgen #{name}.cursor #{CURSORS}/#{name}" if File.exists?("#{name}.cursor") && File.exists?("#{name}.png")
      end
    end
  end
  
  task :configure do
    Dir.chdir(SOURCE) do
      X_COMPLIANT_CURSOR_NAMES.each do |name|
        File.open("#{name}.cursor", 'w') { |file| file.write("24 0 0 #{name}.png\n")} unless File.exists?("#{name}.cursor")
      end
    end
  end
end

namespace :clean do
  desc "Remove the contents of cursors folder"
  task :all do
    Dir.chdir(CURSORS) do
      Dir["*"].each { |file| File.delete file }
    end
  end
end

namespace :convert do
  desc "Convert vector graphics to bitmap images"
  task :all do
    images = Dir["#{SOURCE}/*.svg"]

    images.each do |image|
      sh "inkscape -w 32 -h 32 -f #{image} -e #{image.gsub(".svg", ".png")}"
    end
  end
end
