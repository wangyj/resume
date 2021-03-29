require "rake"

namespace :rst do
  desc "Generate reStructuredText file"
  task :generate do
    puts "Generating reStructuredText file from Markdown"
    system("pandoc -s -w rst resume.markdown -o resume.rst")
    puts "Done"
  end
end

namespace :html do
  desc "Compile stylesheet"
  task :styles do
    puts "Compiling CSS file"
    system("compass compile")
  end

  desc "Generate standalone HTML file"
  task :generate => [:styles] do
    puts "Generating standalone HTML file from Markdown"
    system("pandoc -s resume.markdown -o resume.html -t html5+smart --self-contained --section-divs --template=resume-template.html -T \"Wang Yongjie's Resume\" -c css/main.css")
    system("cp resume.html index.html")
    puts "Done"
  end
end

namespace :tex do
  desc "Generate LaTeX file"
  task :generate do
    puts "Generating LaTeX file from Markdown"
    system("pandoc -s -w context resume.markdown -o resume.tex")
    puts "Done"
  end
end

namespace :pdf do
  desc "Generate PDF file"
  task :generate => ["tex:generate"] do
    puts "Generating PDF file from LaTeX"
    system("pandoc --template=$HOME/Templates/template.tex --pdf-engine=xelatex -s -S resume.markdown -o resume.pdf")
    puts "Done"
  end
end

namespace :rtf do
  desc "Generate RTF file"
  task :generate do
    puts "Generating RTF file from Markdown"
    system("pandoc -s resume.markdown -o resume.rtf")
    puts "Done"
  end
end

namespace :word do
  desc "Generate docx file"
  task :generate do
    puts "Generating docx file from Markdown"
    system("pandoc -s resume.markdown -o resume.docx --reference-doc=resume-reference.docx")
    puts "Done"
  end
end

namespace :odt do
  desc "Generate ODT file"
  task :generate do
    puts "Generating ODT file from Markdown"
    system("pandoc -s resume.markdown -o resume.odt")
    puts "Done"
  end
end

namespace :epub do
  desc "Generate EPUB file"
  task :generate do
    puts "Generating EPUB file from Markdown"
    system("pandoc -s resume.markdown -o resume.epub")
    puts "Done"
  end
end

namespace :asciidoc do
  desc "Generate AsciiDoc file"
  task :generate do
    puts "Generating AsciiDoc file from Markdown"
    system("pandoc -s resume.markdown -t asciidoc -o resume.txt")
    puts "Done"
  end
end

namespace :docbook do
  desc "Generate DocBook file"
  task :generate do
    puts "Generating DocBook file from Markdown"
    system("pandoc -s -w docbook resume.markdown -o resume.db")
    puts "Done"
  end
end

desc "Copy resume to README"
task :readme do
  puts "Copying README"
  system("cp resume.markdown README.markdown")
  puts "Done"
end

desc "Generate all formats"
task :all => [
  # "rst:generate",
  # "html:generate",
  #"pdf:generate",
  # "rtf:generate",
  "word:generate",
  "odt:generate",
  # "epub:generate",
  "asciidoc:generate",
  "docbook:generate",
  "readme"
]

desc "Transfer resume files to web"
task :web do
  puts "Transferring files to web..."
  path = "smt@s17r.com:s17r.com/public"
  system("scp resume.* index.html #{path}/resume")
  system("scp index.html #{path}")
  puts "Done"
end

desc "Commit change"
task :ci do
  puts "Done"
  system("git checkout master")
  system("git add resume.db resume.docx resume.epub resume.html resume.markdown resume.odt resume.pdf resume.rst resume.rtf resume.tex resume.txt README.markdown index.html")
  system("git commit -m 'Update resume files'")
  puts "Done"
end

desc "Push to GitHub"
task :push => [:ci] do
  system("git checkout gh-pages")
  system("git checkout -f master index.html")
  system("git add index.html")
  system("git commit -m 'Update resume on GitHub Pages'")
  system("git push -f")
  system("git checkout master")
end

task :default => ["html:generate"]
