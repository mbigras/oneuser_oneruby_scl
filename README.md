# One user, one ruby

>Build a simple environment with Ruby

## History

Building [mbigras/oneuser_oneruby](https://github.com/mbigras/oneuser_oneruby) was cool
because I learned how to use [postmodern/ruby-install](https://github.com/postmodern/ruby-install) to compile
Ruby from source. However, the process was taking too long to be practical for a quick demo.
I read about [Software Collection](https://www.softwarecollections.org/en/about/) and found the [rh-ruby24](https://www.softwarecollections.org/en/scls/rhscl/rh-ruby24/) package.

Using the Software Collections and the rh-ruby24 I was able to decrease waiting time for a working Ruby environment by X minutes.

## Todo

* time the difference
* learn about how software collections manages the ruby path
* compare and contrast both methods
* Question: can I install both rh-ruby24 and centos-release-scl using items from a list? Would the order matter? [playbook.yml#L21-L27)](https://github.com/mbigras/oneuser_oneruby_scl/blob/3148ea4b046b9d528d558d94901fa042efcbabf3/playbook.yml#L21-L27)


## Usage example

```
export TF_VAR_do_token="$(lpass show --notes do_token)"
lpass logout -f
ssh-keygen -q -b 2048 -t rsa -N '' -f id_rsa
```

```
terraform apply
ansible-playbook playbook.yml
```

```
ip=$(terraform output | awk '/ip/ { print $NF }')
ssh -i id_rsa root@$ip ruby --version
ssh -i id_rsa foo@$ip ruby --version
```

```
terraform destroy -force
rm *.tfstate* id_rsa*
```

## Condensed example

```
terraform apply
ansible-playbook playbook.yml
ip=$(terraform output | awk '/ip/ { print $NF }')
ssh -i id_rsa foo@$ip ruby --version
```

## Links

* https://blog.arkency.com/2012/11/one-app-one-user-one-ruby/
