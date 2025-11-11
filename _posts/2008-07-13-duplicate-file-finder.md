---
title: "Duplicate file finder"
layout: post
date: 2008-07-13 19:30
#image: /assets/images/markdown.jpg
headerImage: false
tag:
- technical
- java
star: false
category: blog
author: varunmehta
description: Duplicate File Finder
---

Disk space is cheap, starting from a 1.2GB hard drive from my first computer to a "spare" 500GB external hard drive, cheap data storage has come a long way. I click a lot of photographs ever since I got my first digital camera, and I store a lot of these photos too (locally), now since 2006 I have over 201,608 photos and some videos. My camera photo number counter has reset twice!!

A few days back I decided to hand over my drive to my brother, since he was leaving soon, I dumped all the stuff on my two laptops, and forgot about them. Of late my wife asked me to pick up good nice pics so we can print them. That's when I realized I had a lot of duplicate photos, now the simplest idea was to find the duplicate file names and delete them, but that was not possible, since I had already reset the counter so I technically had 3 files with the same name and at least 10,000 of them!!

MD5 to the rescue. Since all the photos and movies are binary files, MD5 seemed ideal to me...

> MD5 digests have been widely used in the software world to provide some assurance that a transferred file has arrived intact. For example, file servers often provide a pre-computed MD5 checksum for the files, so that a user can compare the checksum of the downloaded file to it.

So I started my eclipse and churned out a program to scan my HDD and compare MD5 keys and find all duplicates.

The method below generates the MD5 checksum for any file

{% highlight java %}
  private static String generateMD5(String path) throws IOException {
    MessageDigest digest;
    InputStream is = null;
    try {
        digest = MessageDigest.getInstance("MD5");
        is = new FileInputStream(new File(path));
        byte[] buffer = new byte[8192];
        int read = 0;

        while((read = is.read(buffer)) > 0) {
            digest.update(buffer, 0, read);
        }
        byte[] md5sum = digest.digest();
        
        BigInteger bigInt = new BigInteger(1, md5sum);
        return bigInt.toString(16);
    } catch(NoSuchAlgorithmException e) {
        e.printStackTrace();
        throw e;
    } catch(FileNotFoundException e) {
        e.printStackTrace();
        throw e;
    } catch(IOException e) {
        e.printStackTrace();
        throw e;
    } finally {
        is.close();
    }
  }
 {% endhighlight %}
 
Then go ahead and get a list of all the files on your system

missed the code

And finally run the main method.

{% highlight java %}
    public static void main(String[] args) throws Exception {
        List filePaths = new ArrayList();
        File file = new File("/home/varun/workbench/duplicates.csv");
        FileWriter fw = new FileWriter(file);
        SortedMap duplicates = new TreeMap();
        filePaths = generateFileMap("/mnt/datastorage/photos", filePaths);
        for(String path : filePaths) {
            String hash = generateMD5(path);
            if(duplicates.containsKey(hash)) {
                fw.write(path + "," + duplicates.get(hash) + "\n");
            } else {
                duplicates.put(hash, path);
            }
        }
    }
{% endhighlight %}
So go ahead and run this, you can also extend it to generate a list of any kind of duplicate files. Average file size is 1.5 - 2.0 MB

The output file when viewed on Open Office, Google Docs or Excel looks like this

This is what the output looks like. It shows you which file is a duplicate of which other file.

{% highlight bash %}
/mnt/datastorage/Photos/2008/Photos/Halloween NYC 2007/DSC01958.JPG /mnt/datastorage/Photos/2008/Photos/SORT ME/DSC01958.JPG
/mnt/datastorage/Photos/2008/Photos/Halloween NYC 2007/DSC01959.JPG /mnt/datastorage/Photos/2008/Photos/SORT ME/DSC01959.JPG
/mnt/datastorage/Photos/2008/Photos/Halloween NYC 2007/DSC01960.JPG /mnt/datastorage/Photos/2008/Photos/SORT ME/DSC01960.JPG
{% endhighlight %}

## UPDATE 
Ran the program with SHA algorithm also and here are the comparison times.
 * Time for MD5 858,953ms (14.31 minutes)
 * Time for SHA 1,191,656ms (19.80 minutes)

### Bibliography
* http://en.wikipedia.org/wiki/MD5#Applications
* http://en.wikipedia.org/wiki/Md5sum