Want color coding to show up when running Guard through the command line? Add `:cli => "--color"` to your Guardfile as shown below.

`guard 'rspec', :version => 2, :cli => "--color" do
    ... 
end`