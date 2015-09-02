##Rails School:

SQL Injections
-----------------------
vulnerable Active Record methods
  @model.where
  @model.pluck

Safe AR methods
  @model.find_by

User.where("organization = '#{params[:organization]}'")
in field:
  "') OR  true--"
produces:
  SELECT "users".* FROM "users" WHERE (organization = '"') OR  true--"')

NEVER use string interpolation for SQL queries

fix with:
  User.where(organization: params[:organization])

If you have to use SQL:
  User.where("organization = ?", params[:organization]) # Prepared Statements

Mass Assignment
-----------------------
Github got owned by this

Adding in another field in the form and submitting it along, not checking for new fields.

strong_params, attr_accessor, or whitelisting fields solves this.
config.action_controller.permit_all_parameters not being set to true solves this by default

CSRF
-------------------------
APIs usually turn this off, don't do that. 
http://stackoverflow.com/questions/7203304/warning-cant-verify-csrf-token-authenticity-rails
