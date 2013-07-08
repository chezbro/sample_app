# A sample Guardfile
# More info at https://github.com/guard/guard#readme
require 'active_support/core_ext'

guard 'rspec', :version => 2, :all_after_pass => false, :cli => "--drb" do

watch(%r{ˆapp/controllers/(.+)(controller)\.rb$}) do|m|
  ["spec/routing/#{m[1]} routing spec.rb", "spec/#{m[2]}s/#{m[1]} #{m[2]} spec.rb", "spec/acceptance/#{m[1]} spec.rb",
  (m[1][/ pages/] ? "spec/requests/#{m[1]} spec.rb" :
  "spec/requests/#{m[1].singularize} pages spec.rb")]
  end
watch(%r{ˆapp/views/(.+)/}) do|m|
  "spec/requests/#{m[1].singularize} pages spec.rb"
  end


guard :rspec do
  watch(%r{^spec/.+_spec\.rb$})
  watch(%r{^lib/(.+)\.rb$})     { |m| "spec/lib/#{m[1]}_spec.rb" }
  watch('spec/spec_helper.rb')  { "spec" }
  end
end


guard 'spork', :cucumber_env => { 'RAILS_ENV' => 'test' }, :rspec_env => { 'RAILS_ENV' => 'test' } do
  watch('config/application.rb')
  watch('config/environment.rb')
  watch('config/environments/test.rb')
  watch(%r{^config/initializers/.+\.rb$})
  watch('Gemfile.lock')
  watch('spec/spec_helper.rb') { :rspec }
  watch('test/test_helper.rb') { :test_unit }
  watch(%r{features/support/}) { :cucumber }
end
