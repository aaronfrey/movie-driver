# Movie Driver

## Local Development

### Requirements

- [Composer](https://getcomposer.org/)
- [VirtualBox 6.x](https://www.virtualbox.org/wiki/Downloads)
- [Vagrant >=2.2.6](https://www.vagrantup.com/downloads.html)
- [Laravel Homestead](https://laravel.com/docs/6.x/homestead)

## Laravel Homestead
### Installation
- Install [VirtualBox 6.x](https://www.virtualbox.org/wiki/Downloads)
- Install [Vagrant](https://www.vagrantup.com/downloads.html)
- Install the `laravel/homestead` box for Vagrant:
```bash
$ vagrant box add laravel/homestead
```
- Install Homestead:
```bash
$ git clone https://github.com/laravel/homestead.git c:\projects\Homestead
$ cd c:\projects\Homestead
$ git checkout release
$ init.bat
```
- Add the following configuration to `Homestead.yaml` in `c:\projects\Homestead`
```yaml
folders:
    - map: /projects/movie-driver
      to: /home/vagrant/movie-driver

sites:
    - map: movie-driver.test
      to: /home/vagrant/movie-driver/public
```

- Add the following to `C:\Windows\System32\drivers\etc\hosts`
```
192.168.10.10  movie-driver.test
```
- Run `$vagrant up` in the terminal from the Homestead root

## Laravel Site
### Installation

- Clone this repository to `c:\projects\movie-driver`
- Copy the `.env` file to the root of the application.
- SSH into Homestead and install Composer dependancies from the `/movie-driver` directory:
```bash
$ composer install
```
- Install NPM dependancies from the host machine in `c:\projects\movie-driver`:
```bash
$ npm install && npm run watch
```
- SSH into Homestead and create the PostgreSQL database
```bash
vagrant@homestead:~$ psql -U homestead -h localhost # password is 'secret'
homestead=# create database moviedriver;
homestead=# exit

vagrant@homestead:~/movie-driver$ php artisan migrate
vagrant@homestead:~/movie-driver$ php artisan db:seed
```
