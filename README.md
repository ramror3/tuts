*** Default Route
**************************===**************************
ddddddddddddddddddddddddd
ssssssssssssssssssssssssssss
sssd

match ':controller(/:action(/:id))', :via => :get

match ':controller(/:action(/:id(.:format)))', :via => :get

*** Root Route

root :to => "demo#index"

root "demo#index"

*** Render

Its take the request from other same and other controller

def index
  	render('hello')
  end

*** Redirect

Its take the request from other location or other controller also.

def other_hello
  	redirect_to(:controller => 'demo', :action => 'index')
end

def you
  	redirect_to("http://youtube.com")
end

*** Template file naming
hello.html.erb
 Template name: hello

 Process with: erb

 Output format: HTML, XML, JS, Jquery, Json


*** Parameters hash
params
	Contains all GET and POST variables

*** HashWithIndifferentAccess

	params need to be matched.

params[:id]

params['id']

*** Creating a database in MySQL

		==> access mysql: mysql -d root -p

  SHOW DATABASES;

  CREATE DATABASE db_name;

  USE db_name;

  DROP DATABASE db_name;

*** Connecting db as root
	Creating a New MySQL User

	GRANT ALL PRIVILEGES ON tuts.* TO 'tuts'@'localhost' IDENTIFIED	BY 'mypassword';

	SHOW GRANTS FOR 'tuts'@'localhost';

	mysql -u tuts -p tuts_development (then enter ur pwd)

*** rake db:schema:dump

Login to db: => mysql -u tuts -p tuts_development
				SHOW TABLES;
				SHOW FIELDS FROM users;
				SHOW FIELDS FROM schema_migrations;
				SELECT * FROM schema_migrations;

	=> rake db:migrate VERSION=0 (Its reverting the migation)
	=> rake db:migrate VERSION=20171102092538 (Its re-generate the migration)

	====================******************************=======================
	***One-to-One
	subject has_one :page
	page belongs_to :subject

	first_page = Page.new(...)
	subject.page = first_page
	subject.page
	first_page.subject
	subject.page.destroy
	subject.page

	====================******************************=======================
	***One-to-Many
	subject has_many :pages
	Page belongs_to :subject

	***has_many_methods

	subject.pages
	subject.pages << page
	subject.pages = [page, page, page]
	subject.pages.delete(page)
	subject.pages.destroy(page)
	subject.pages.clear
	subject.pages.empty?
	subject.pages.size
	first_page = Page.new(...)
	subject.pages << first_page  (append the ids and sub_id)
	second_page = Page.new(...)
	subject.pages << second_page
	second_page.subject
	subject.pages.empty? #false
	subject.pages.size
	subject.pages.delete(second_page)
	subject.pages.count

	====================******************************=======================
	***Many-to_Many
	AdminUser-Page

	AdminUser has_and_belongs_to_many :pages
	Page has_and_belongs_to_many :admin_users

	************ Join Table Naming **********first_table_name+ +second_table_name*******

	@ Project - Collaborator
		collaborators_projects

	@ BlogPost - Category
		blog_post_categories

	@ AdminUser - Page
		admin_users_pages
	*** rails g migration CreateAdminUsersPagesJoin ***

	page = Page.find(2)
	page.editors
		#<ActiveRecord::Associations::CollectionProxy []>
	AdminUser.all
		 #<ActiveRecord::Relation []>
	me = AdminUser.create(...)
	page.editors << me
	page.editors
	me.pages

	***Mant-to-Many Associtions Rich***

	Course => has_many :course_enrollments
	Students => has_many :course_enrollments
	CourseEnrollment => belongs_to :course
						belongs_to :student

	* AdminUser - Section
	AdminUser => has_many :section_edits
	SectionEdit => belongs_to :admin_user
	Section => has_many :section_edits
	SectionEdit => belongs_to :section

	me.section_edits
	Section.all
	section = Section.create(...)
	section.section_edits
	edit = SectionEdit.new
	edit.summary = "Test Edit"

	====================******************************=======================
	*** has_many :through
	* AdminUser - Section

		AdminUser has_many :section_edits
		AdminUser has_many :section, :through => :section_edits

		Section has_many :section_edits
		Section has_many :admin_users, :through => :section_edits	
