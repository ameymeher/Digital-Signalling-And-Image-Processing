
<!DOCTYPE html
  PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN">
<html><head>
      <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
   <!--
This HTML was auto-generated from MATLAB code.
To make changes, update the MATLAB code and republish this document.
      --><title>finalHistogram</title><meta name="generator" content="MATLAB 9.3"><link rel="schema.DC" href="http://purl.org/dc/elements/1.1/"><meta name="DC.date" content="2018-06-11"><meta name="DC.source" content="finalHistogram.m"><style type="text/css">
html,body,div,span,applet,object,iframe,h1,h2,h3,h4,h5,h6,p,blockquote,pre,a,abbr,acronym,address,big,cite,code,del,dfn,em,font,img,ins,kbd,q,s,samp,small,strike,strong,sub,sup,tt,var,b,u,i,center,dl,dt,dd,ol,ul,li,fieldset,form,label,legend,table,caption,tbody,tfoot,thead,tr,th,td{margin:0;padding:0;border:0;outline:0;font-size:100%;vertical-align:baseline;background:transparent}body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}blockquote:before,blockquote:after,q:before,q:after{content:'';content:none}:focus{outine:0}ins{text-decoration:none}del{text-decoration:line-through}table{border-collapse:collapse;border-spacing:0}

html { min-height:100%; margin-bottom:1px; }
html body { height:100%; margin:0px; font-family:Arial, Helvetica, sans-serif; font-size:10px; color:#000; line-height:140%; background:#fff none; overflow-y:scroll; }
html body td { vertical-align:top; text-align:left; }

h1 { padding:0px; margin:0px 0px 25px; font-family:Arial, Helvetica, sans-serif; font-size:1.5em; color:#d55000; line-height:100%; font-weight:normal; }
h2 { padding:0px; margin:0px 0px 8px; font-family:Arial, Helvetica, sans-serif; font-size:1.2em; color:#000; font-weight:bold; line-height:140%; border-bottom:1px solid #d6d4d4; display:block; }
h3 { padding:0px; margin:0px 0px 5px; font-family:Arial, Helvetica, sans-serif; font-size:1.1em; color:#000; font-weight:bold; line-height:140%; }

a { color:#005fce; text-decoration:none; }
a:hover { color:#005fce; text-decoration:underline; }
a:visited { color:#004aa0; text-decoration:none; }

p { padding:0px; margin:0px 0px 20px; }
img { padding:0px; margin:0px 0px 20px; border:none; }
p img, pre img, tt img, li img, h1 img, h2 img { margin-bottom:0px; } 

ul { padding:0px; margin:0px 0px 20px 23px; list-style:square; }
ul li { padding:0px; margin:0px 0px 7px 0px; }
ul li ul { padding:5px 0px 0px; margin:0px 0px 7px 23px; }
ul li ol li { list-style:decimal; }
ol { padding:0px; margin:0px 0px 20px 0px; list-style:decimal; }
ol li { padding:0px; margin:0px 0px 7px 23px; list-style-type:decimal; }
ol li ol { padding:5px 0px 0px; margin:0px 0px 7px 0px; }
ol li ol li { list-style-type:lower-alpha; }
ol li ul { padding-top:7px; }
ol li ul li { list-style:square; }

.content { font-size:1.2em; line-height:140%; padding: 20px; }

pre, code { font-size:12px; }
tt { font-size: 1.2em; }
pre { margin:0px 0px 20px; }
pre.codeinput { padding:10px; border:1px solid #d3d3d3; background:#f7f7f7; }
pre.codeoutput { padding:10px 11px; margin:0px 0px 20px; color:#4c4c4c; }
pre.error { color:red; }

@media print { pre.codeinput, pre.codeoutput { word-wrap:break-word; width:100%; } }

span.keyword { color:#0000FF }
span.comment { color:#228B22 }
span.string { color:#A020F0 }
span.untermstring { color:#B20000 }
span.syscmd { color:#B28C00 }

.footer { width:auto; padding:10px 0px; margin:25px 0px 0px; border-top:1px dotted #878787; font-size:0.8em; line-height:140%; font-style:italic; color:#878787; text-align:left; float:none; }
.footer p { margin:0px; }
.footer a { color:#878787; }
.footer a:hover { color:#878787; text-decoration:underline; }
.footer a:visited { color:#878787; }

table th { padding:7px 5px; text-align:left; vertical-align:middle; border: 1px solid #d6d4d4; font-weight:bold; }
table td { padding:7px 5px; text-align:left; vertical-align:top; border:1px solid #d6d4d4; }





  </style></head><body><div class="content"><pre class="codeinput"><span class="comment">%Coded by: Amey Meher</span>
<span class="comment">%For queries drop a mail at: amey.meher@somaiya.edu</span>
</pre><pre class="codeinput"><span class="comment">%Original Image Probability and frequency distribution</span>
<span class="comment">%Read image</span>
image1 = imread(<span class="string">'sample1.jpg'</span>);

<span class="comment">%Use the function</span>
[totalPixels,redCounts,grayLevels] = histogram(image1,1);
[totalPixels,greenCounts,grayLevels] = histogram(image1,2);
[totalPixels,blueCounts,grayLevels] = histogram(image1,3);

pixelArray = cat(1,redCounts,greenCounts,blueCounts);
pixelArray = reshape(pixelArray,[256,3]);

<span class="comment">%Plot the Probability distribution and finding the cumulative frequency</span>
[redProbability,redCumulative] = equalize(redCounts,totalPixels);
[greenProbability,greenCumulative] = equalize(greenCounts,totalPixels);
[blueProbability,blueCumulative] = equalize(blueCounts,totalPixels);

probabilityArray = cat(1,redProbability,greenProbability,blueProbability);
probabilityArray = reshape(probabilityArray,[256,3]);
</pre><pre class="codeinput"><span class="comment">%Equalizing the image</span>
<span class="comment">%Make the newImage</span>
[rows,columns,numberOfChannels] = size(image1);
<span class="keyword">for</span> i=1:rows
    <span class="keyword">for</span> j=1:columns
        newImageRed(i,j) = 255 * redCumulative(image1(i,j,1) + 1);
        newImageGreen(i,j) = 255 * greenCumulative(image1(i,j,2) + 1);
        newImageBlue(i,j) = 255 * blueCumulative(image1(i,j,3) + 1);
    <span class="keyword">end</span>
<span class="keyword">end</span>

newImageRed = uint8(newImageRed);
newImageGreen = uint8(newImageGreen);
newImageBlue = uint8(newImageBlue);
newImage = cat(3,newImageRed,newImageGreen,newImageBlue);

<span class="comment">%Use the function</span>
[newTotalPixels,redNewCounts,newGrayLevels] = histogram(newImage,1);
[newTotalPixels,greenNewCounts,newGrayLevels] = histogram(newImage,2);
[newTotalPixels,blueNewCounts,newGrayLevels] = histogram(newImage,3);
newPixelArray = cat(1,redNewCounts,greenNewCounts,blueNewCounts);
newPixelArray = reshape(newPixelArray,[256,3]);

<span class="comment">%Plot the Probability distribution and finding the cumulative frequency</span>
[redNewProbability,redNewCumulative] = equalize(redNewCounts,newTotalPixels);
[greenNewProbability,greenNewCumulative] = equalize(greenNewCounts,newTotalPixels);
[blueNewProbability,blueNewCumulative] = equalize(blueNewCounts,newTotalPixels);
newProbabilityArray = cat(1,redNewProbability,greenNewProbability,blueNewProbability);
newProbabilityArray = reshape(newProbabilityArray,[256,3]);
</pre><pre class="codeinput"><span class="comment">%Plotting the graphs</span>
<span class="comment">%Plot the histogram</span>
plotHistogram(grayLevels,pixelArray,3,2,3,<span class="string">'Pixels'</span>,<span class="string">'Frequency'</span>,<span class="string">'Frequency Distribution'</span>);
plotHistogram(grayLevels,probabilityArray,3,2,5,<span class="string">'Pixels'</span>,<span class="string">'Probability'</span>,<span class="string">'Probability Distribution'</span>);
plotHistogram(newGrayLevels,newPixelArray,3,2,4,<span class="string">'Pixels'</span>,<span class="string">'Frequency'</span>,<span class="string">'Equalized Frequency Distribution'</span>);
plotHistogram(newGrayLevels,newProbabilityArray,3,2,6,<span class="string">'Pixels'</span>,<span class="string">'Probability'</span>,<span class="string">'Equalized Probability Distribution'</span>);

<span class="comment">%Displaying before and after image</span>
subplot(3,2,1);
imshow(image1);
title(<span class="string">'Original Image'</span>);
subplot(3,2,2);
imshow(newImage);
title(<span class="string">'Equalized Image'</span>);
</pre><pre class="codeinput"><span class="comment">%Histogram function to calculate the counts of the pixels and the range of</span>
<span class="comment">%gray levels</span>

<span class="keyword">function</span> [totalPixels,counts,grayLevels] = histogram(image,channel)
    counts = zeros(1,256);
    grayLevels = 0:255;
    [rows, columns,numberOfChannels] = size(image);
    totalPixels = rows * columns;
    <span class="keyword">for</span> i=1:rows
        <span class="keyword">for</span> j=1:columns
            grayLevel = image(i,j,channel);
            counts(grayLevel + 1) = counts(grayLevel + 1) + 1;
        <span class="keyword">end</span>
    <span class="keyword">end</span>
<span class="keyword">end</span>
</pre><pre class="codeinput"><span class="comment">%Equalize function to calculate cumulative frequency distribution</span>
<span class="keyword">function</span> [probability,cumulative] = equalize(counts,totalPixels)
    probability = zeros(1,256);
    cumulative = zeros(1,256);
    <span class="keyword">for</span> i=1:256
       probability(i) = counts(i) / totalPixels;
       <span class="keyword">if</span>(i == 1)
           cumulative(i) = probability(i);
       <span class="keyword">else</span>
           cumulative(i) = cumulative(i-1) + probability(i);
       <span class="keyword">end</span>
    <span class="keyword">end</span>
<span class="keyword">end</span>
</pre><pre class="codeinput"><span class="comment">%For plotting the histogram in a subplot using bar structure</span>
<span class="keyword">function</span> plotHistogram(grayLevels,counts,i,j,k,xLabel,yLabel,name)
    subplot(i,j,k);
    bar(grayLevels,counts);
    xlabel(xLabel, <span class="string">'FontSize'</span>, 8);
    ylabel(yLabel, <span class="string">'FontSize'</span>, 8);
    title(name, <span class="string">'FontSize'</span>, 8);
<span class="keyword">end</span>
</pre><img vspace="5" hspace="5" src="finalHistogram_01.png" alt=""> <p class="footer"><br><a href="http://www.mathworks.com/products/matlab/">Published with MATLAB&reg; R2017b</a><br></p></div><!--
##### SOURCE BEGIN #####
%%
%Coded by: Amey Meher
%For queries drop a mail at: amey.meher@somaiya.edu

%%
%Original Image Probability and frequency distribution
%Read image
image1 = imread('sample1.jpg');

%Use the function
[totalPixels,redCounts,grayLevels] = histogram(image1,1);
[totalPixels,greenCounts,grayLevels] = histogram(image1,2);
[totalPixels,blueCounts,grayLevels] = histogram(image1,3);

pixelArray = cat(1,redCounts,greenCounts,blueCounts);
pixelArray = reshape(pixelArray,[256,3]);
        
%Plot the Probability distribution and finding the cumulative frequency
[redProbability,redCumulative] = equalize(redCounts,totalPixels);
[greenProbability,greenCumulative] = equalize(greenCounts,totalPixels);
[blueProbability,blueCumulative] = equalize(blueCounts,totalPixels);

probabilityArray = cat(1,redProbability,greenProbability,blueProbability);
probabilityArray = reshape(probabilityArray,[256,3]);

%%
%Equalizing the image
%Make the newImage
[rows,columns,numberOfChannels] = size(image1);
for i=1:rows
    for j=1:columns
        newImageRed(i,j) = 255 * redCumulative(image1(i,j,1) + 1);
        newImageGreen(i,j) = 255 * greenCumulative(image1(i,j,2) + 1);
        newImageBlue(i,j) = 255 * blueCumulative(image1(i,j,3) + 1);
    end
end

newImageRed = uint8(newImageRed);
newImageGreen = uint8(newImageGreen);
newImageBlue = uint8(newImageBlue);
newImage = cat(3,newImageRed,newImageGreen,newImageBlue);

%Use the function
[newTotalPixels,redNewCounts,newGrayLevels] = histogram(newImage,1);
[newTotalPixels,greenNewCounts,newGrayLevels] = histogram(newImage,2);
[newTotalPixels,blueNewCounts,newGrayLevels] = histogram(newImage,3);
newPixelArray = cat(1,redNewCounts,greenNewCounts,blueNewCounts);
newPixelArray = reshape(newPixelArray,[256,3]);

%Plot the Probability distribution and finding the cumulative frequency
[redNewProbability,redNewCumulative] = equalize(redNewCounts,newTotalPixels);
[greenNewProbability,greenNewCumulative] = equalize(greenNewCounts,newTotalPixels);
[blueNewProbability,blueNewCumulative] = equalize(blueNewCounts,newTotalPixels);
newProbabilityArray = cat(1,redNewProbability,greenNewProbability,blueNewProbability);
newProbabilityArray = reshape(newProbabilityArray,[256,3]);



%%
%Plotting the graphs
%Plot the histogram
plotHistogram(grayLevels,pixelArray,3,2,3,'Pixels','Frequency','Frequency Distribution');
plotHistogram(grayLevels,probabilityArray,3,2,5,'Pixels','Probability','Probability Distribution');
plotHistogram(newGrayLevels,newPixelArray,3,2,4,'Pixels','Frequency','Equalized Frequency Distribution');
plotHistogram(newGrayLevels,newProbabilityArray,3,2,6,'Pixels','Probability','Equalized Probability Distribution');

%Displaying before and after image
subplot(3,2,1);
imshow(image1);
title('Original Image');
subplot(3,2,2);
imshow(newImage);
title('Equalized Image');
%%
%Histogram function to calculate the counts of the pixels and the range of
%gray levels

function [totalPixels,counts,grayLevels] = histogram(image,channel)
    counts = zeros(1,256);
    grayLevels = 0:255;
    [rows, columns,numberOfChannels] = size(image);
    totalPixels = rows * columns;
    for i=1:rows
        for j=1:columns
            grayLevel = image(i,j,channel);
            counts(grayLevel + 1) = counts(grayLevel + 1) + 1;
        end
    end
end

%%
%Equalize function to calculate cumulative frequency distribution
function [probability,cumulative] = equalize(counts,totalPixels)
    probability = zeros(1,256);
    cumulative = zeros(1,256);
    for i=1:256
       probability(i) = counts(i) / totalPixels;
       if(i == 1)
           cumulative(i) = probability(i);
       else
           cumulative(i) = cumulative(i-1) + probability(i);
       end
    end
end

%%
%For plotting the histogram in a subplot using bar structure
function plotHistogram(grayLevels,counts,i,j,k,xLabel,yLabel,name)
    subplot(i,j,k);
    bar(grayLevels,counts);
    xlabel(xLabel, 'FontSize', 8);
    ylabel(yLabel, 'FontSize', 8);
    title(name, 'FontSize', 8);
end



##### SOURCE END #####
--></body></html>