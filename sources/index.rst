MinecraftMediaLibrary
=================================================

MinecraftMediaLibrary is a library used to display media to players
such as pictures, audio, videos, and other forms of media. It uses
a variety of displays that are customizable depending on the user's
needs.

Quickstart Guide
=================================================

Importing MinecraftMediaLibrary into a project
=================================================

First, add Jitpack because the repository is hosted there.

.. tabs::

   .. group-tab:: Maven

      .. code:: xml

         <repositories>
    		   <repository>
    		     <id>jitpack.io</id>
    	  	   <url>https://jitpack.io</url>
    		   </repository>
    	   </repositories>

   .. group-tab:: Gradle (Groovy)

      .. code:: groovy

         allprojects {
    		   repositories {
    		  	 maven { url 'https://jitpack.io' }
    		   }
    	   }

   .. group-tab:: Gradle (Kotlin)

      .. code:: kotlin

         allprojects {
    		   repositories {
    		     maven { url 'https://jitpack.io' }
    		   }
    	   }

Then, add the actual library repo itself.

.. tabs::

   .. group-tab:: Maven

      .. code:: xml

         <dependency>
    	      <groupId>com.github.MinecraftMediaLibrary</groupId>
    	      <artifactId>MinecraftMediaLibrary</artifactId>
    	      <version>-SNAPSHOT</version>
    	   </dependency>

   .. group-tab:: Gradle (Groovy)

      .. code:: groovy

         dependencies {
    	     implementation 'com.github.MinecraftMediaLibrary:MinecraftMediaLibrary:-SNAPSHOT'
    	   }

   .. group-tab:: Gradle (Kotlin)

      .. code:: kotlin

         dependencies {
           implementation 'com.github.MinecraftMediaLibrary:MinecraftMediaLibrary:-SNAPSHOT'
         }
