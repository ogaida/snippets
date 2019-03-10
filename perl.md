```perl
#!/usr/bin/env perl
# https://www.heise.de/ix/artikel/Oder-so-aehnlich-1765809.html
# https://metacpan.org/pod/Image::Hash
use Image::Hash;
use File::Slurp;
# Read a image from the command line
my @files = <*>;
%hashes=();
%sizes=();

foreach my $file (@files) {
  print ".";
  my $image = read_file( $file, binmode => ':raw' ) ;
  my $ihash = Image::Hash->new($image);
  # Calculate the perception hash
  my $p = $ihash->phash();
  my $size = -s $file;
  print "$p,$size,$file,\n";
  if ($hashes{$p}){
    print "existiert bereits...\n";
    my $first_file=$hashes{$p};
    if ($sizes{$file} > $sizes{$first_file}){
      $hashes{$p}=$file;
      $sizes{$file}=$size;
      unlink $first_file;
    }else{
      unlink $file;
    }
  }else{
    $hashes{$p}=$file;
    $sizes{$file}=$size;
  }
}
```
