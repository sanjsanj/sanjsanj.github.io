---
layout: post
title: Pre-Course
---
Today was the final day of our four-week long precourse and it's been a very steep learning curve so far.  Now we are prepared to go through our 12-week preparation at Makers Academy to become ace coders with all the hot skills new tech wants.  But the pre-preparation didn't begin here.
{% highlight ruby linenos %}
puts "Hello, World!"
puts "How original..."
{% endhighlight %}

Before we got accepted on the course we had to learn some basic coding and attend an interview that consisted of an informal one-to-one and some pair programming to test what we had learned so far.  I thought I failed miserably on the coding part, only knowing the answers to a few of the dozen or so challenges put before us.  But as it turns out knowing the answers isn't what's important, it the willingness to communicate, ability to find the answers and acceptance that we won't ever know all the answers.

Since then I have truly come to understand the significance of that statement.

But I digress, so I actually got accepted on the course which thrilled me to bits.  I was eager to learn and wanted to get some new high level skills under my belt.  After that, the first week of our precourse was to learn the basics of the command-line interface.  Terminal on Macs and Bash in Linux.  We also had a brief primer on Unix commands and VI.

My hardcore coder friends tell me VI(Visual Interface) is THE BEST!  I'm sure it is.

At the end of that week we got a challenge, this is a theme with the course, at the end of most weeks you will get a chance to apply what you've learned during the week.  This seems like a very effective way to learn.  Learn a bit of theory, put it in to practice right away on the same day, rinse and repeat, then at the end of the weekly cycle you get a much larger and more significant challenge to really get to grips with the knowledge.

The second week was about Github, the popular version-control system.  I absolutely fell in love with Git and have become highly addicted to filling those green boxes and keeping up my high-scoring streak of commits.

The weekly challenge for Git was really fun, it included creating, adding, commiting and pushing local files from our terminals up to the origin repo on Git.  This obviously after having to initialise the local repo and creating the remote ones and syncing the two up.  We also covered checking out, merging, rebasing, branching and bunch of more delicious candy.

The third week is where we started to learn coding proper!  It was Ruby week, and it was going to be tough.  Materials included Learn Ruby The Hard Way, Ruby Mony, Ruby Kickstart, Codewars, Ruby Koans and more.  The weekly challenge was probably our hugest challenge to date, to complete the first two sessions of Ruby Kickstart, if you've ever tried then you might appreciate how difficult this would be for pure beginners to Ruby and to coding.

The fourth and final week was further reinforcement of our Ruby skills, any further time to practice this was and still is very welcome.  We had to create a student directory that could, at first, store a hard-coded list of students and allow us to perform menial retrieval tasks on them.  Then we set it up so that we could add further values to each student, such as hobbies, cohort, etc.  Then we used YAML to to store and retrieve the student directory in a text file.  Then we made an interactive CLI interface for users to interact with, to store, retrieve and do all sorts of other amazing things with!

{% highlight ruby linenos %}
require "csv"
@students = []

def print_header
  print "The students of March 2015 cohort at Makers Academy\n"
  print "--------------\n"
end

def print_students_list
  @students.each_with_index do |student, index|
    linewidth = 30
    print "#{index + 1}. #{student[:name]} of #{student[:cohort]} cohort".ljust(linewidth)
    print "#{student[:hobby]} hobby".center(linewidth)
    print "and COB is #{student[:cob]}\n".rjust(linewidth)
  end
end

def print_footer
  @students.length == 1 ? pluralize = "student" : pluralize = "students"
  print "Overall, we have #{@students.length} great #{pluralize}\n"
end

def input_student_data
  print "Please enter the names of the student, their cohort, their hobby and country of birth seperated by ',' without any spaces\n"
  print "To finish, just hit enter twice\n"
  name = STDIN.gets.strip
  while !name.empty? do
    studary = name.split(",")
    @students << {:name => studary[0], :cohort => studary[1].to_sym, :hobby => studary[2], :cob => studary[3]}
    @students.length == 1 ? pluralize = "student" : pluralize = "students"
    print "Now we have #{@students.length} #{pluralize}\n"
    name = STDIN.gets.strip
  end
  @students
end

def interactive_menu
  loop do
    try_load_students
    print_menu
    process(STDIN.gets.chomp)
  end
end

def print_menu
  puts "1. Input the students"
  puts "2. Show the students"
  puts "3. Save the list to file (append)"
  puts "4. Load the list from file"
  puts "9. Exit"
end
  
def process(selection)
  case selection
    when "1"
      input_student_data
    when "2"
      show_students
    when "3"
      save_students
    when "4"
      load_students
    when "9"
      exit
    else
      puts "I don't know what you meant, try again"
  end
end

def show_students
  print_header
  print_students_list
  print_footer
end

def save_students
  puts "Enter filename or leave blank to use students.csv"
  savefile = gets.chomp
  savefile = "students.csv" if savefile == ""
  CSV.open(savefile, "a+") do |csv|
    @students.each do |student|
      csv << [student[:name], student[:cohort], student[:hobby], student[:cob]]
    end
  end
  puts "#{@students.length} students' data saved in #{savefile}"
end

def load_students(filename = "students.csv")
  puts "Enter name of file to load from or leave blank to use students.csv"
  loadfile = gets.chomp
  loadfile = "students.csv" if loadfile == ""
  CSV.foreach(loadfile) do |row|
    name, cohort, hobby, cob = row
    @students << {:name => name, :cohort => cohort.to_sym, :hobby => hobby, :cob => cob }
  end
  puts "Loaded #{@students.length} students from #{loadfile}"
end

def try_load_students
  filename = ARGV.first
  return if filename.nil?
  if File.exists?(filename)
    load_students(filename)
    puts "Loaded #{@students.length} students from #{filename}"
  else
    puts "Sorry, #{filename} doesn't exist"
    exit
  end
end

puts "This program was executed by #{$0}"
interactive_menu
{% endhighlight %}

Damn, it feels good to be a coder.

Sandi Metz's POODR is high on our reading list too.  We have been taught to understand and appreciate Object-Oriented Programming and all the things we're tasked with are to help build on those fundamentals.

By now I've interacted with most of my cohort online and they seem like a really awesome and mixed bunch of people, I think we're going to enjoy this.
