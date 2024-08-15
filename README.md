# Actuarial-Science-#!/usr/bin/perl
use strict;
use warnings;
    
my @sensor_data = (10, 12, 15, 20);
my $n = scalar @sensor_data;
    
sub integrated_sensor_data {
my @data = @_;
my $sum = 0;
$sum += $_ for @data;
return $sum;
    }
    
sub actuating_function {
my $D_t = shift;
return $D_t * 0.9;
    }
    
sub filtering_function {
my $D_t = shift;
return $D_t - 1;
    }
    
sub determining_function {
my $F_t = shift;
return $F_t * 1.1;
    }
    
sub guiding_function {
my $S_t = shift;
return $S_t / 2;
    }
    
sub robustness_function {
my ($D_t, $state_conditions) = @_;
return $D_t * (1 - $state_conditions);
    }
    
my $state_conditions = 0.1;
my $performance_decline_rate = 0.05;
my $time = 10;
    
my $D_t = integrated_sensor_data(@sensor_data);
my $A_t = actuating_function($D_t);
my $F_t = filtering_function($D_t);
my $S_t = determining_function($F_t);
my $G_t = guiding_function($S_t);
my $R_t = robustness_function($D_t, $state_conditions);
    
my $P_t = $R_t - ($performance_decline_rate * $time);
    
print "Integrated Sensor Data: $D_t\n";
print "Actuating Value: $A_t\n";
print "Filtered Data: $F_t\n";
print "Determined State: $S_t\n";
print "Guided Value: $G_t\n";
print "Robustness: $R_t\n";
print "Overall System Performance: $P_t\n";
1;
