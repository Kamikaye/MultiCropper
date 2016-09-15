//Import Image Sequence
print("\\Clear");
print("1. Find Stack and click the first image ! \n 2. Select a folder for the cropped stack(s) \n 3.  Select your future stacks  \n Adjust during the blink phase and hit t to add \n 4. start cropping by holding ALT to break blink loop !");
run("Image Sequence...", "sort use");
roiManager("Reset");
//In case import fails or no stack was selected, exit the macro
if (nSlices==1) exit("Stack required ! The virtual stack can be opened using File>Import>Image Sequence, File>Import>TIFF Virtual Stack or File>Import>Raw.");

//Whre to put the stacks
sdir = getDirectory("Where to put the cropped stacks ?");

setTool("rectangle");

//Blinkroutine
waitForUser("Select your regions of interest (Roots, Hypocotyls, leave some space around for tolerance) \n Hit t to add another ROI ! \n Hold ALT to confirm ! \n Zoom and scrolling possible!");
altkey = false;
do   {
  Stack.setSlice(nSlices-1);
  wait(1000);
  Stack.setSlice(1);
  wait(1000);

  if (isKeyDown("alt") == true) altkey = true;
} while (altkey == false);
  
//Work through the stack, duplicate each image, cut selected ROIs from it and save them in subfolders
n = roiManager("count");
for (i=0; i<n; i++) {
     segment = "segment_"+i + File.separator;
     ddir = sdir+segment;
     File.makeDirectory(ddir);
     roiManager("select", i);
     run("Duplicate...", "title = segment duplicate range=1-["+n+"]");
     run("Image Sequence... ", "format=TIFF name=["+segment+"] start=0 digits=5 use save=["+ddir+"]");
close();
  } 
showMessage("Done !");
