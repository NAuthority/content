---
title: The "codecs" parameter in common media types
slug: Web/Media/Formats/codecs_parameter
tags:
  - Audio
  - Codecs
  - Containers
  - MIME
  - MIME Types
  - Media
  - Media Types
  - Parameter
  - Types
  - Video
  - Web
  - formats
---
<div>{{QuickLinksWithSubpages("/en-US/docs/Web/Media")}}</div>

<p>At a fundamental level, you can specify the type of a media file using a simple {{Glossary("MIME")}} type, such as <code>video/mp4</code> or <code>audio/mpeg</code>. However, many media types—especially those that support video tracks—can benefit from the ability to more precisely describe the format of the data within them. For instance, just describing a video in an <a href="/en-US/docs/Web/Media/Formats/Containers#mp4">MPEG-4</a> file with the MIME type <code>video/mp4</code> doesn't say anything about what format the actual media within takes.</p>

<p>For that reason, the <code>codecs</code> parameter can be added to the MIME type describing media content. With it, container-specific information can be provided. This information may include things like the profile of the video codec, the type used for the audio tracks, and so forth.</p>

<p><span class="seoSummary">This guide briefly examines the syntax of the media type <code>codecs</code> parameter and how it's used with the MIME type string to provide details about the contents of audio or video media beyond indicating the container type.</span></p>

<h2 id="General_syntax">General syntax</h2>

<p>A basic MIME media type is expressed by stating the type of media (<code>audio</code>, <code>video</code>, etc), then a slash character (<code>/</code>), then the container format used to contain the media:</p>

<dl>
 <dt><code>audio/mpeg</code></dt>
 <dd>An audio file using the <a href="/en-US/docs/Web/Media/Formats/Containers#mpeg">MPEG</a> file type, such as an MP3.</dd>
 <dt><code>video/ogg</code></dt>
 <dd>A video file using the <a href="/en-US/docs/Web/Media/Formats/Containers#ogg">Ogg</a> file type.</dd>
 <dt><code>video/mp4</code></dt>
 <dd>A video file using the <a href="/en-US/docs/Web/Media/Formats/Containers#mp4">MPEG-4</a> file type.</dd>
 <dt><code>video/quicktime</code></dt>
 <dd>A video file in Apple's <a href="/en-US/docs/Web/Media/Formats/Containers#quicktime">QuickTime</a> format. As noted elsewhere, this format was once commonly used on the web but no longer is, since it required a plugin to use.</dd>
</dl>

<p>However, each of these MIME types is vague. All of these file types support a variety of codecs, and those codecs may have any number of profiles, levels, and other configuration factors. For this reason, you can add the <code>codecs</code> parameter to the media type.</p>

<p>To do so, append a semicolon (<code>;</code>) followed by <code>codecs=</code> and then the string describing the format of the contents of the file. Some media types only let you specify the names of the codecs to use, while others allow you to specify various constraints on those codecs as well. You can specify multiple codecs by separating them with commas.</p>

<dl>
 <dt><code>audio/ogg; codecs=vorbis</code></dt>
 <dd>An <a href="/en-US/docs/Web/Media/Formats/Containers#ogg">Ogg</a> file containing a <a href="/en-US/docs/Web/Media/Formats/Audio_codecs#vorbis">Vorbis</a> audio track.</dd>
 <dt><code>video/webm; codecs="vp8, vorbis"</code></dt>
 <dd>A <a href="/en-US/docs/Web/Media/Formats/Containers#webm">WebM</a> file containing <a href="/en-US/docs/Web/Media/Formats/Video_codecs#vp8">VP8</a> video and/or <a href="/en-US/docs/Web/Media/Formats/Audio_codecs#vorbis">Vorbis</a> audio.</dd>
 <dt><code>video/mp4; codecs="avc1.4d002a"</code></dt>
 <dd>An <a href="/en-US/docs/Web/Media/Formats/Containers#mp4">MPEG-4</a> file containing <a href="/en-US/docs/Web/Media/Formats/Video_codecs#avc_(h.264)">AVC</a> (H.264) video, Main Profile, Level 4.2.</dd>
</dl>

<p>As is the case with any MIME type parameter, <code>codecs</code> must be changed to <code>codecs*</code> (note the asterisk character, <code>*</code>) if any of the properties of the codec use special characters which must be percent-encoded per {{RFC(2231, "MIME Parameter Value and Encoded Word Extensions", 4)}}. You can use the JavaScript {{jsxref("Global_Objects/encodeURI", "encodeURI()")}} function to encode the parameter list; similarly, you can use {{jsxref("Global_Objects/decodeURI", "decodeURI()")}} to decode a previously encoded parameter list.</p>

<div class="notecard note">
<p><strong>Note:</strong> When the <code>codecs</code> parameter is used, the specified list of codecs must include every codec used for the contents of the file. The list may also contain codecs not present in the file.</p>
</div>

<h2 id="Codec_options_by_container">Codec options by container</h2>

<p>The containers below support extended codec options in their <code>codecs</code> parameters:</p>

<ul>
 <li>{{anch("iso_base_media_file_format_mp4_quicktime_and_3gp", "3GP")}}</li>
 <li>{{anch("AV1")}}</li>
 <li>{{anch("iso_base_media_file_format_mp4_quicktime_and_3gp", "ISO BMFF")}}</li>
 <li>{{anch("iso_base_media_file_format_mp4_quicktime_and_3gp", "MPEG-4")}}</li>
 <li>{{anch("iso_base_media_file_format_mp4_quicktime_and_3gp", "QuickTime")}}</li>
 <li>{{anch("WebM")}}</li>
</ul>

<p>Several of the links above go to the same section; that's because those media types are all based on ISO Base Media File Format (ISO BMFF), so they share the same syntax.</p>

<h3 id="AV1">AV1</h3>

<p>The syntax of the <code>codecs</code> parameter for AV1 is defined the <a href="https://aomediacodec.github.io/av1-isobmff">AV1 Codec ISO Media File Format Binding</a> specification, section 5: <a href="https://aomediacodec.github.io/av1-isobmff/#codecsparam">Codecs Parameter String</a>.</p>

<pre class="brush: plain">av01.P.LLT.DD[.M[.CCC[.cp[.tc[.mc[.F]]]]]]</pre>

<p>This codec parameter string's components are described in more detail in the table below. Each component is a fixed number of characters long; if the value is less than that length, it must be padded with leading zeros.</p>

<table class="standard-table">
 <caption>AV1 codec parameter string components</caption>
 <thead>
  <tr>
   <th scope="col">Component</th>
   <th scope="col">Details</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>P</code></td>
   <td>
    <p>The one-digit profile number:</p>

    <table class="standard-table">
     <caption>AV1 profile numbers</caption>
     <thead>
      <tr>
       <th scope="col">Profile number</th>
       <th scope="col">Description</th>
      </tr>
     </thead>
     <tbody>
      <tr>
       <td>0</td>
       <td>"Main" profile; supports YUV 4:2:0 or monochrome bitstreams with bit depth of 8 or 10 bits per component.</td>
      </tr>
      <tr>
       <td>1</td>
       <td>"High" profile adds support for 4:4:4 chroma subsampling.</td>
      </tr>
      <tr>
       <td>2</td>
       <td>"Professional" profile adds support for 4:2:2 chroma subsampling and 12 bit per component color.</td>
      </tr>
     </tbody>
    </table>
   </td>
  </tr>
  <tr>
   <td><code>LL</code></td>
   <td>The two-digit level number, which is converted to the X.Y format level format, where <code>X = 2 + (LL &gt;&gt; 2)</code> and <code>Y = LL &amp; 3</code>. See <a href="https://aomediacodec.github.io/av1-spec/#levels">Appendix A, section 3</a> in the AV1 Specification for details.</td>
  </tr>
  <tr>
   <td><code>T</code></td>
   <td>The one-character tier indicator. For the Main tier (<code>seq_tier</code> equals 0), this character is the letter <code>M</code>. For the High tier (<code>seq_tier</code> is 1), this character is the letter <code>H</code>. The High tier is only available for level 4.0 and up.</td>
  </tr>
  <tr>
   <td><code>DD</code></td>
   <td>The two-digit component bit depth. This value must be one of 8, 10, or 12; which values are valid varies depending on the profile and other properties.</td>
  </tr>
  <tr>
   <td><code>M</code></td>
   <td>The one-digit monochrome flag; if this is 0, the video includes the U and V planes in addition to the Y plane. Otherwise, the video data is entirely in the Y plane and is therefore monochromatic. See {{SectionOnPage("/en-US/docs/Web/Media/Formats/Video_concepts", "YUV")}} for details on how the YUV color system works. The default value is 0 (not monochrome).</td>
  </tr>
  <tr>
   <td><code>CCC</code></td>
   <td>
    <p><code>CCC</code> indicates the chroma subsampling as three digits. The first digit is <code>subsampling_x</code>, the second is <code>subsampling_y</code>. If both of those are 1, the third is the value of <code>chroma_sample_position</code>; otherwise, the third digit is always 0. This, combined with the <code>M</code> component, can be used to construct the chroma subsampling format:</p>

    <table class="standard-table">
     <caption>Determining the chroma subsampling format</caption>
     <thead>
      <tr>
       <th scope="col">subsampling_x</th>
       <th scope="col">subsampling_y</th>
       <th scope="col">Monochrome flag</th>
       <th scope="col">Chroma subsampling format</th>
      </tr>
     </thead>
     <tbody>
      <tr>
       <td>0</td>
       <td>0</td>
       <td>0</td>
       <td>YUV 4:4:4</td>
      </tr>
      <tr>
       <td>1</td>
       <td>0</td>
       <td>0</td>
       <td>YUV 4:2:2</td>
      </tr>
      <tr>
       <td>1</td>
       <td>1</td>
       <td>0</td>
       <td>YUV 4:2:0</td>
      </tr>
      <tr>
       <td>1</td>
       <td>1</td>
       <td>1</td>
       <td>YUV 4:0:0 (Monochrome)</td>
      </tr>
     </tbody>
    </table>

    <p>The third digit in <code>CCC</code> indicates the chroma sample position, with a value of 0 indicating that the position is unknown and must be separately provided during decoding; a value of 1 indicating that the sample position is horizontally colocated with the (0, 0) luma sample; and a value of 2 indicating that the sample position is colocated with (0, 0) luma.</p>

    <p>The default value is <code>110</code> (4:2:0 chroma subsampling).</p>
   </td>
  </tr>
  <tr>
   <td><code>cp</code></td>
   <td>The two-digit <code>color_primaries</code> value indicates the color system used by the media. For example, BT.2020/BT.2100 color, as used for HDR video, is <code>09</code>. The information for this—and for each of the remaining components—is found in the <a href="https://aomediacodec.github.io/av1-spec/#color-config-semantics">Color config semantics section</a> of the AV1 specification. The default value is <code>01</code> (ITU-R BT.709).</td>
  </tr>
  <tr>
   <td><code>tc</code></td>
   <td>The two-digit <code>transfer_characteristics</code> value. This value defines the function used to map the gamma (delightfully called the "opto-electrical transfer function" in technical parlance) from the source to the display. For example, 10-bit BT.2020 is <code>14</code>. The default value is <code>01</code> (ITU-R BT.709).</td>
  </tr>
  <tr>
   <td><code>mc</code></td>
   <td>The two-digit <code>matrix_coefficients</code> constant selects the matrix coefficients used to convert the red, blue, and green channels into luma and chroma signals. For example, the standard coefficients used for BT.709 are indicated using the value <code>01</code>. The default value is <code>01</code> (ITU-R BT.709).</td>
  </tr>
  <tr>
   <td><code>F</code></td>
   <td>A one-digit flag indicating whether the color should be allowed to use the full range of possible values (<code>1</code>), or should be constrained to those values considered legal for the specified color configuration (that is, the <strong>studio swing representation</strong>). The default is 0 (use the studio swing representation).</td>
  </tr>
 </tbody>
</table>

<p>All fields from <code>M</code> (monochrome flag) onward are optional; you may stop including fields at any point (but can't arbitrarily leave out fields). The default values are included in the table above. Some example AV1 codec strings:</p>

<dl>
 <dt><code>av01.2.15M.10.0.100.09.16.09.0</code></dt>
 <dd>AV1 Professional Profile, level 5.3, Main tier, 10 bits per color component, 4:2:2 chroma subsampling using ITU-R BT.2100 color primaries, transfer characteristics, and YCbCr color matrix. The studio swing representation is indicated.</dd>
 <dt><code>av01.0.15M.10</code></dt>
 <dd>AV1 Main Profile, level 5.3, Main tier, 10 bits per color component. The remaining properties are taken from the defaults: 4:2:0 chroma subsampling, BT.709 color primaries, transfer characteristics, and matrix coefficients. Studio swing representation.</dd>
</dl>

<h3 id="iso_base_media_file_format_mp4_quicktime_and_3gp">ISO Base Media File Format: MP4, QuickTime, and 3GP</h3>

<p>All media types based upon the {{interwiki("wikipedia", "ISO Base Media File Format")}} (ISO BMFF) share the same syntax for the <code>codecs</code> parameter. These media types include <a href="/en-US/docs/Web/Media/Formats/Containers#mp4">MPEG-4</a> (and, in fact, the <a href="/en-US/docs/Web/Media/Formats/Containers#quicktime">QuickTime</a> file format upon which MPEG-4 is based) as well as <a href="/en-US/docs/Web/Media/Formats/Containers#3gp">3GP</a>. Both video and audio tracks can be described using the <code>codecs</code> parameter with the following MIME types:</p>

<table class="standard-table">
 <caption>Base MIME types supporting the ISO BMFF codecs parameter</caption>
 <thead>
  <tr>
   <th scope="col">MIME type</th>
   <th scope="col">Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>audio/3gpp</code></td>
   <td>3GP audio ({{RFC(3839, "MIME Type Registrations for 3rd generation Partnership Project (3GP) Multimedia files")}})</td>
  </tr>
  <tr>
   <td><code>video/3gpp</code></td>
   <td>3GP video ({{RFC(3839, "MIME Type Registrations for 3rd generation Partnership Project (3GP) Multimedia files")}})</td>
  </tr>
  <tr>
   <td><code>audio/3gp2</code></td>
   <td>3GP2 audio ({{RFC(4393, "MIME Type Registrations for 3GPP2 Multimedia files")}})</td>
  </tr>
  <tr>
   <td><code>video/3gp2</code></td>
   <td>3GP2 video ({{RFC(4393, "MIME Type Registrations for 3GPP2 Multimedia files")}})</td>
  </tr>
  <tr>
   <td><code>audio/mp4</code></td>
   <td>MP4 audio ({{RFC(4337, "MIME Type Registration for MPEG-4")}})</td>
  </tr>
  <tr>
   <td><code>video/mp4</code></td>
   <td>MP4 audio ({{RFC(4337, "MIME Type Registration for MPEG-4")}})</td>
  </tr>
  <tr>
   <td><code>application/mp4</code></td>
   <td>Non-audiovisual media encapsulated in MPEG-4</td>
  </tr>
 </tbody>
</table>

<p>Each codec described by the <code>codecs</code> parameter can be specified either as the container's name (<code>3gp</code>, <code>mp4</code>, <code>quicktime</code>, etc.) or as the container name plus additional parameters to specify the codec and its configuration. Each entry in the codec list may contain some number of components, separated by periods (<code>.</code>).</p>

<p>The syntax for the value of <code>codecs</code> varies by codec; however, it always starts with the codec's four-character identifier, a period separator (<code>.</code>), followed by the Object Type Indication (OTI) value for the specific data format. For most codecs, the OTI is a two-digit hexadecimal number; however, it's six hexadecimal digits for <a href="/en-US/docs/Web/Media/Formats/Video_codecs#avc_(h.264)">AVC (H.264)</a>.</p>

<p>Thus, the syntaxes for each of the supported codecs look like this:</p>

<dl>
 <dt><code>cccc[.pp]*</code> (Generic ISO BMFF)</dt>
 <dd>Where <code>cccc</code> is the four-character ID for the codec and <code>pp</code> is where zero or more two-character encoded property values go.</dd>
 <dt><code>mp4a.oo[.A]</code> (MPEG-4 audio)</dt>
 <dd>Where <code>oo</code> is the Object Type Indication value describing the contents of the media more precisely and <code>A</code> is the one-digit <em>audio</em> OTI. The possible values for the OTI can be found on the MP4 Registration Authority web site's <a href="https://mp4ra.org/#/object_types">Object Types page</a>. For example, Opus audio in an MP4 file is <code>mp4a.ad</code>. For further details, see {{anch("MPEG-4 audio")}}.</dd>
 <dt><code>mp4v.oo[.V]</code> (MPEG-4 video)</dt>
 <dd>Here, <code>oo</code> is again the OTI describing the contents more precisely, while <code>V</code> is the one-digit <em>video</em> OTI.</dd>
 <dt><code>avc1.oo[.PPCCLL]</code> (AVC video)</dt>
 <dd>
 <p><code>oo</code> is the OTI describing the contents, while <code>PPCCLL</code> is six hexadecimal digits specifying the profile number (<code>PP</code>), constraint set flags (<code>CC</code>), and level (<code>LL</code>). See {{anch("AVC profiles")}} for the possible values of <code>PP</code>.</p>

 <p>The constraint set flags byte is comprised of one-bit Boolean flags, with the most significant bit being referred to as flag 0 (or <code>constraint_set0_flag</code>, in some resources), and each successive bit being numbered one higher. Currently, only flags 0 through 2 are used; the other five bits <em>must</em> be zero. The meanings of the flags vary depending on the profile being used.</p>

 <p>The level is a fixed-point number, so a value of <code>14</code> (decimal 20) means level 2.0 while a value of <code>3D</code> (decimal 61) means level 6.1. Generally speaking, the higher the level number, the more bandwidth the stream will use and the higher the maximum video dimensions are supported.</p>
 </dd>
</dl>

<h4 id="AVC_profiles">AVC profiles</h4>

<p>The following are the AVC profiles and their profile numbers for use in the <code>codecs</code> parameter, as well as the value to specify for the constraints component, <code>CC</code>.</p>

<table class="standard-table">
 <caption>Specifying an AVC profiles using the profile ID and constraints components of the <code>codecs</code> parameter</caption>
 <thead>
  <tr>
   <th scope="col">Profile</th>
   <th scope="col">Number (Hex)</th>
   <th scope="col">Constraints byte</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>Constrained Baseline Profile (CBP)</strong><br>
    CBP is primarily a solution for scenarios in which resources are constrained, or resource use needs to be controlled to minimize the odds of the media performing poorly.</td>
   <td><code>42</code></td>
   <td><code>40</code></td>
  </tr>
  <tr>
   <td><strong>Baseline Profile (BP)</strong><br>
    Similar to CBP but with more data loss protections and recovery capabilities. This is not as widely used as it was before CBP was introduced. All CBP streams are considered to also be BP streams.</td>
   <td><code>42</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Extended Profile (XP)</strong><br>
    Designed for streaming video over the network, with high compression capability and further improvements to data robustness and stream switching.</td>
   <td><code>58</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Main Profile (MP)</strong><br>
    The profile used for standard-definition digital television being broadcast in MPEG-4 format. <em>Not</em> used for high-definition television broadcasts. This profile's importance has faded since the introduction of the High Profile—which was added for HDTV use—in 2004.</td>
   <td><code>4D</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>High Profile (HiP)</strong><br>
    Currently, HiP is the primary profile used for broadcast and disc-based HD video; it's used both for HD TV broadcasts and for  Blu-Ray video.</td>
   <td><code>64</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Progressive High Profile (PHiP)</strong><br>
    Essentially High Profile without support for field coding.</td>
   <td><code>64</code></td>
   <td><code>08</code></td>
  </tr>
  <tr>
   <td><strong>Constrained High Profile</strong><br>
    PHiP, but without support for bi-predictive slices ("B-slices").</td>
   <td><code>64</code></td>
   <td><code>0C</code></td>
  </tr>
  <tr>
   <td><strong>High 10 Profile (Hi10P)</strong><br>
    High Profile, but with support for up to 10 bits per color component.</td>
   <td><code>6E</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>High 4:2:2 Profile (Hi422P)</strong><br>
    Expands upon Hi10P by adding support for 4:2:2 chroma subsampling along with up to10 bits per color component.</td>
   <td><code>7A</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>High 4:4:4 Predictive Profile (Hi444PP)</strong><br>
    In addition to the capabilities included in Hi422P, Hi444PP adds support for 4:4:4 chroma subsampling (in which no color information is discarded). Also includes support for up to 14 bits per color sample and efficient lossless region coding. The option to encode each frame as three separate color planes (that is, each color's data is stored as if it were a single monochrome frame).</td>
   <td><code>F4</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>High 10 Intra Profile</strong><br>
    High 10 constrained to all-intra-frame use. Primarily used for professional apps.</td>
   <td><code>6E</code></td>
   <td><code>10</code></td>
  </tr>
  <tr>
   <td><strong>High 4:2:2 Intra Profile</strong><br>
    The Hi422 Profile with all-intra-frame use.</td>
   <td><code>7A</code></td>
   <td><code>10</code></td>
  </tr>
  <tr>
   <td><strong>High 4:4:4 Intra Profile</strong><br>
    The High 4:4:4 Profile constrained to use only intra frames.</td>
   <td><code>F4</code></td>
   <td><code>10</code></td>
  </tr>
  <tr>
   <td><strong>CAVLC 4:4:4 Intra Profile</strong><br>
    The High 4:4:4 Profile constrained to all-intra use, and to using only CAVLC entropy coding.</td>
   <td><code>44</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Scalable Baseline Profile</strong><br>
    Intended for use with video conferencing as well as surveillance and mobile uses, the {{interwiki("wikipedia", "SVC")}} Baseline Profile is based on AVC's Constrained Baseline profile. The base layer within the stream is provided at a high quality level, with some number of secondary substreams that offer alternative forms of the same video for use in various constrained environments. These may include any combination of reduced resolution, reduced frame rate, or increased compression levels.</td>
   <td><code>53</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Scalable Constrained Baseline Profile</strong><br>
    Primarily used for real-time communication applications. Not yet supported by WebRTC, but an extension to the WebRTC API <a href="https://github.com/w3c/webrtc-svc">to allow SVC</a> is in development.</td>
   <td><code>53</code></td>
   <td><code>04</code></td>
  </tr>
  <tr>
   <td><strong>Scalable High Profile</strong><br>
    Meant mostly for use in broadcast and streaming applications. The base (or highest quality) layer must conform to the AVC High Profile.</td>
   <td><code>56</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Scalable Constrained High Profile</strong><br>
    A subset of the Scalable High Profile designed mainly for real-time communticions.</td>
   <td><code>56</code></td>
   <td><code>04</code></td>
  </tr>
  <tr>
   <td><strong>Scalable High Intra Profile</strong><br>
    Primarily useful only for production applications, this profile supports only all-intra usage.</td>
   <td><code>56</code></td>
   <td><code>20</code></td>
  </tr>
  <tr>
   <td><strong>Stereo High Profile</strong><br>
    The Stereo High Profile provides stereoscopic video using two renderings of the scene (left eye and right eye). Otherwise, provides the same features as the High profile.</td>
   <td><code>80</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Multiview High Profile</strong><br>
    Supports two or more views using both temporal and MVC inter-view prediction. <em>Does not support</em> field pictures or macroblock-adaptive frame-field coding.</td>
   <td><code>76</code></td>
   <td><code>00</code></td>
  </tr>
  <tr>
   <td><strong>Multiview Depth High Profile</strong><br>
    Based on the High Profile, to which the main substream must adhere. The remaining substreams must match the Stereo High Profile.</td>
   <td><code>8A</code></td>
   <td><code>00</code></td>
  </tr>
 </tbody>
</table>

<h4 id="MPEG-4_audio">MPEG-4 audio</h4>

<p>When the value of an entry in the <code>codecs</code> list begins with <code>mp4a</code>, the syntax of the value should be:</p>

<pre class="brush: plain">mp4a.oo[.A]</pre>

<p>Here, <code>oo</code> is the two-digit hexadecimal Object Type Indication which specifies the codec class being used for the media. The OTIs are assigned by the <a href="https://mp4ra.org/">MP4 Registration Authority</a>, which maintains a <a href="https://mp4ra.org/#/object_types">list of the possible OTI values</a>. A special value is <code>40</code>; this indicates that the media is MPEG-4 audio (ISO/IEC 14496 Part 3). In order to be more specific still, a third component—the Audio Object Type—is added for OTI <code>40</code> to narrow the type down to a specific subtype of MPEG-4.</p>

<p>The Audio Object Type is specified as a one or two digit <em>decimal</em> value (unlike most other values in the <code>codecs</code> parameter, which use hexadecimal). For example, MPEG-4's AAC-LC has an audio object type number of <code>2</code>, so the full <code>codecs</code> value representing AAC-LC is <code>mp4a.40.2</code>.</p>

<p>Thus, ER AAC LC, whose Audio Object Type is 17, can be represented using the full <code>codecs</code> value <code>mp4a.40.17</code>. Single digit values can be given either as one digit (which is the best choice, since it will be the most broadly compatible) or with a leading zero padding it to two digits, such as <code>mp4a.40.02</code>.</p>

<div class="notecard note">
<p><strong>Note:</strong> The specification originally mandated that the Audio Object Type number in the third component be only one decimal digit. However, amendments to the specification over time extended the range of these values well beyond one decimal digit, so now the third parameter may be either one or two digits. Padding values below 10 with a leading <code>0</code> is optional. Older implementations of MPEG-4 codecs may not support two-digit values, however, so using a single digit when possible will maximize compatibility.</p>
</div>

<p>The Audio Object Types are defined in ISO/IEC 14496-3 subpart 1, section 1.5.1. The table below provides a basic list of the Audio Object Types and in the case of the more common object ypes provides a list of the profiles supporting it, but you should refer to the specification for details if you need to know more about the inner workings of any given MPEG-4 audio type.</p>

<table class="standard-table">
 <caption>MPEG-4 audio object types</caption>
 <thead>
  <tr>
   <th scope="col">ID</th>
   <th scope="col">Audio Object Type</th>
   <th scope="col">Profile support</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>0</code></td>
   <td>NULL</td>
   <td></td>
  </tr>
  <tr>
   <td><code>1</code></td>
   <td>AAC Main</td>
   <td>Main</td>
  </tr>
  <tr>
   <td><code>2</code></td>
   <td>AAC LC (Low Complexity)</td>
   <td>Main, Scalable, HQ, LD v2, AAC, HE-AAC, HE-AAC v2</td>
  </tr>
  <tr>
   <td><code>3</code></td>
   <td>AAC SSR (Scalable Sampling Rate)</td>
   <td>Main</td>
  </tr>
  <tr>
   <td><code>4</code></td>
   <td>AAC LTP (Long Term Prediction)</td>
   <td>Main, Scalable, HQ</td>
  </tr>
  <tr>
   <td><code>5</code></td>
   <td>SBR (Spectral Band Replication)</td>
   <td>HE-AAC, HE-AAC v2</td>
  </tr>
  <tr>
   <td><code>6</code></td>
   <td>AAC Scalable</td>
   <td>Main, Scalable, HQ</td>
  </tr>
  <tr>
   <td><code>7</code></td>
   <td>TwinVQ (Coding for ultra-low bit rates)</td>
   <td>Main, Scalable</td>
  </tr>
  <tr>
   <td><code>8</code></td>
   <td>CELP (Code-Excited Linear Prediction)</td>
   <td>Main, Scalable, Speech, HQ, LD</td>
  </tr>
  <tr>
   <td><code>9</code></td>
   <td>HVXC (Harmonic Vector Excitation Coding)</td>
   <td>Main, Scalable, Speech, LD</td>
  </tr>
  <tr>
   <td><code>10</code> – <code>11</code></td>
   <td><em>Reserved</em></td>
   <td></td>
  </tr>
  <tr>
   <td><code>12</code></td>
   <td>TTSI (Text to Speech Interface)</td>
   <td>Main, Scalable, Speech, Synthetic, LD</td>
  </tr>
  <tr>
   <td><code>13</code></td>
   <td>Main Synthetic</td>
   <td>Main, Synthetic</td>
  </tr>
  <tr>
   <td><code>14</code></td>
   <td>Wavetable Synthesis</td>
   <td></td>
  </tr>
  <tr>
   <td><code>15</code></td>
   <td>General MIDI</td>
   <td></td>
  </tr>
  <tr>
   <td><code>16</code></td>
   <td>Algorithmic Synthesis and Audio Effects</td>
   <td></td>
  </tr>
  <tr>
   <td><code>17</code></td>
   <td>ER AAC LC (Error Resilient AAC Low-Complexity)</td>
   <td>HQ, Mobile Internetworking</td>
  </tr>
  <tr>
   <td><code>18</code></td>
   <td><em>Reserved</em></td>
   <td></td>
  </tr>
  <tr>
   <td><code>19</code></td>
   <td>ER AAC LTP (Error Resilient AAC Long Term Prediction)</td>
   <td>HQ</td>
  </tr>
  <tr>
   <td><code>20</code></td>
   <td>ER AAC Scalable (Error Resilient AAC Scalable)</td>
   <td>Mobile Internetworking</td>
  </tr>
  <tr>
   <td><code>21</code></td>
   <td>ER TwinVQ (Error Resilient TwinVQ)</td>
   <td>Mobile Internetworking</td>
  </tr>
  <tr>
   <td><code>22</code></td>
   <td>ER BSAC (Error Reslient Bit-Sliced Arithmetic Coding)</td>
   <td>Mobile Internetworking</td>
  </tr>
  <tr>
   <td><code>23</code></td>
   <td>ER AAC LD (Error Resilient AAC Low-Delay; used for two-way communication)</td>
   <td>LD, Mobile Internetworking</td>
  </tr>
  <tr>
   <td><code>24</code></td>
   <td>ER CELP (Error Resilient Code-Excited Linear Prediction)</td>
   <td>HQ, LD</td>
  </tr>
  <tr>
   <td><code>25</code></td>
   <td>ER HVXC (Error Resilient Harmonic Vector Excitation Coding)</td>
   <td>LD</td>
  </tr>
  <tr>
   <td><code>26</code></td>
   <td>ER HILN (Error Resilient Harmonic and Individual Line plus Noise)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>27</code></td>
   <td>ER Parametric (Error Resilient Parametric)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>28</code></td>
   <td>SSC (Sinusoidal Coding)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>29</code></td>
   <td>PS (Parametric Stereo)</td>
   <td>HE-AAC v2</td>
  </tr>
  <tr>
   <td><code>30</code></td>
   <td>MPEG Surround</td>
   <td></td>
  </tr>
  <tr>
   <td><code>31</code></td>
   <td><em>Escape</em></td>
   <td></td>
  </tr>
  <tr>
   <td><code>32</code></td>
   <td>MPEG-1 Layer-1</td>
   <td></td>
  </tr>
  <tr>
   <td><code>33</code></td>
   <td>MPEG-1 Layer-2 (MP2)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>34</code></td>
   <td>MPEG-1 Layer-3 (MP3)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>35</code></td>
   <td>DST (Direct Stream Transfer)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>36</code></td>
   <td>ALS (Audio Lossless)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>37</code></td>
   <td>SLS (Scalable Lossless)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>38</code></td>
   <td>SLS Non-core (Scalable Lossless Non-core)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>39</code></td>
   <td>ER AAC ELD (Error Resilient AAC Enhanced Low Delay)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>40</code></td>
   <td>SMR Simple (Symbolic Music Representation Simple)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>41</code></td>
   <td>SMR Main (Symbolic Music Representation Main)</td>
   <td></td>
  </tr>
  <tr>
   <td><code>42</code></td>
   <td><em>Reserved</em></td>
   <td></td>
  </tr>
  <tr>
   <td><code>43</code></td>
   <td>
     <p>SAOC (Spatial Audio Object Coding)</p>
     <p>Defined in <a href="https://www.iso.org/standard/54838.html">ISO/IEC 14496-3:2009/Amd.2:2010(E)</a>.</p></td>
   <td></td>
  </tr>
  <tr>
   <td><code>44</code></td>
   <td>
     <p>LD MPEG Surround (Low Delay MPEG Surround)</p>
     <p>Defined in <a href="https://www.iso.org/standard/54838.html">ISO/IEC 14496-3:2009/Amd.2:2010(E)</a>.</p>
   </td>
   <td></td>
  </tr>
  <tr>
   <td><code>45</code> and up</td>
   <td><em>Reserved</em></td>
   <td></td>
  </tr>
 </tbody>
</table>

<h3 id="WebM">WebM</h3>

<p>The basic form for a WebM <code>codecs</code> parameter is to list one or more of the four WebM codecs by name, separated by commas. The table below shows some examples:</p>

<table class="standard-table">
 <caption>Examples of classic WebM MIME types with <code>codecs</code> parameter</caption>
 <thead>
  <tr>
   <th scope="col">MIME type</th>
   <th scope="col">Description</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>video/webm;codecs="vp8"</code></td>
   <td>A WebM video with VP8 video in it; no audio is specified.</td>
  </tr>
  <tr>
   <td><code>video/webm;codecs="vp9"</code></td>
   <td>A WebM video with VP9 video in it.</td>
  </tr>
  <tr>
   <td><code>audio/webm;codecs="vorbis"</code></td>
   <td>Vorbis audio in a WebM container.</td>
  </tr>
  <tr>
   <td><code>audio/webm;codecs="opus"</code></td>
   <td>Opus audio in a WebM container.</td>
  </tr>
  <tr>
   <td><code>video/webm;codecs="vp8,vorbis"</code></td>
   <td>A WebM container with VP8 video and Vorbis audio.</td>
  </tr>
  <tr>
   <td><code>video/webm;codecs="vp9,opus"</code></td>
   <td>A WebM container with VP9 video and Opus audio.</td>
  </tr>
 </tbody>
</table>

<p>The strings <code>vp8.0</code> and <code>vp9.0</code> also work, but are not recommended.</p>

<h4 id="ISO_Base_Media_File_Format_syntax">ISO Base Media File Format syntax</h4>

<p>As part of a move toward a standardized and powerful format for the <code>codecs</code> parameter, WebM is moving toward describing <em>video</em> content using a syntax based on that defined by the <a href="#iso-bmff">ISO Base Media File Format</a>. This syntax is defined in <a href="https://www.webmproject.org/vp9/mp4">VP Codec ISO Media File Format Binding</a>, in the section <a href="https://www.webmproject.org/vp9/mp4/#codecs-parameter-string">Codecs Parameter String</a>. The audio codec continues to be indicated as either <code>vorbis</code> or <code>opus</code>.</p>

<p>In this format, the <code>codecs</code> parameter's value begins with a four-character code identifying the codec being used in the container, which is then followed by a series of period (<code>.</code>) separated two-digit values.</p>

<pre class="brush: plain">cccc.PP.LL.DD.CC[.cp[.tc[.mc[.FF]]]]</pre>

<p>The first five components are required; everything from <code>cp</code> (color primaries) onward is optional; you can stop including components at any point from then onward. Each of these components is described in the following table. Following the table are some examples.</p>

<table class="standard-table">
 <caption>WebM codecs parameter components</caption>
 <thead>
  <tr>
   <th scope="col">Component</th>
   <th scope="col">Details</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>cccc</code></td>
   <td>
    <p>A four-character code indicating which indicates which of the possible codecs is being described. Potential values are:</p>

    <table class="standard-table">
     <caption>Four-character codes for WebM-supported codecs</caption>
     <thead>
      <tr>
       <th scope="col">Four-character code</th>
       <th scope="col">Codec</th>
      </tr>
     </thead>
     <tbody>
      <tr>
       <td><code>vp08</code></td>
       <td>VP8</td>
      </tr>
      <tr>
       <td><code>vp09</code></td>
       <td>VP9</td>
      </tr>
      <tr>
       <td><code>vp10</code></td>
       <td>VP10</td>
      </tr>
     </tbody>
    </table>
   </td>
  </tr>
  <tr>
   <td><code>PP</code></td>
   <td>
    <p>The two-digit profile number, padded with leading zeroes if necessary to be exactly two digits.</p>

    <table class="standard-table">
     <caption>WebM profile numbers</caption>
     <thead>
      <tr>
       <th scope="col">Profile</th>
       <th scope="col">Description</th>
      </tr>
     </thead>
     <tbody>
      <tr>
       <td><code>00</code></td>
       <td>Only 4:2:0 (chroma subsampled both horizontally and vertically). Allows only 8 bits per color component.</td>
      </tr>
      <tr>
       <td><code>01</code></td>
       <td>All chroma subsampling formats are allowed. Allows only 8 bits per color component.</td>
      </tr>
      <tr>
       <td><code>02</code></td>
       <td>Only 4:2:0 (chroma subsampled both horizontally and vertically). Supports 8, 10, or 12 bits per color sample component.</td>
      </tr>
      <tr>
       <td><code>03</code></td>
       <td>All chroma subsampling formats are allowed. Supports 8, 10, or 12 bits per color sample component.</td>
      </tr>
     </tbody>
    </table>
   </td>
  </tr>
  <tr>
   <td><code>LL</code></td>
   <td>The two-digit level number. The level number is a fixed-point notation, where the first digit is the ones digit, and the second digit represents tenths. For example, level 3 is <code>30</code> and level 6.1 is <code>61</code>.</td>
  </tr>
  <tr>
   <td><code>DD</code></td>
   <td>The bit depth of the luma and color component values; permitted values are 8, 10, and 12.</td>
  </tr>
  <tr>
   <td><code>CC</code></td>
   <td>
    <p>A two-digit value indicating which chroma subsampling format to use. The following table lists permitted values; see {{SectionOnPage("en-US/docs/Web/Media/Formats/Video_concepts", "Chroma subsampling")}} for additional information about this topic and others.</p>

    <table class="standard-table">
     <caption>WebM chroma subsampling identifiers</caption>
     <thead>
      <tr>
       <th scope="col">Value</th>
       <th scope="col">Chroma subsampling format</th>
      </tr>
     </thead>
     <tbody>
      <tr>
       <td><code>00</code></td>
       <td>4:2:0 with the chroma samples sited interstitially between the pixels</td>
      </tr>
      <tr>
       <td><code>01</code></td>
       <td>4:2:0 chroma subsampling with the samples colocated with luma (0, 0)</td>
      </tr>
      <tr>
       <td><code>02</code></td>
       <td>4:2:2 chroma subsampling (4 out of each 4 horizontal pixels' luminance are used)</td>
      </tr>
      <tr>
       <td><code>03</code></td>
       <td>4:4:4 chroma subsampling (every pixel's luminance and chrominance are both retained)</td>
      </tr>
      <tr>
       <td><code>04</code></td>
       <td><em>Reserved</em></td>
      </tr>
     </tbody>
    </table>
   </td>
  </tr>
  <tr>
   <td><code>cp</code></td>
   <td>
    <p>A two-digit integer specifying which of the color primaries from Section 8.1 of the <a href="https://www.itu.int/rec/T-REC-H.273/en">ISO/IEC 23001-8:2016</a> standard. This component, and every component after it, is optional.</p>

    <p>The possible values of the color primaries component are:</p>

    <table class="standard-table">
     <caption>ISO/IEC Color primary identifiers</caption>
     <thead>
      <tr>
       <th scope="col">Value</th>
       <th scope="col">Details</th>
      </tr>
     </thead>
     <tbody>
      <tr>
       <td><code>00</code></td>
       <td><em>Reserved for future use by ITU or ISO/IEC</em></td>
      </tr>
      <tr>
       <td><code>01</code></td>
       <td>BT.709, sRGB, sYCC. BT.709 is the standard for high definition (HD) television; sRGB is the most common color space used for computer displays. Broadcast BT.709 uses 8-bit color depth with the legal range being from 16 (black) to 235 (white).</td>
      </tr>
      <tr>
       <td><code>02</code></td>
       <td>Image characteristics are unknown, or are to be determined by the application</td>
      </tr>
      <tr>
       <td><code>03</code></td>
       <td><em>Reserved for future use by ITU or ISO/IEC</em></td>
      </tr>
      <tr>
       <td><code>04</code></td>
       <td>BT.470 System M, NTSC (standard definition television in the United States)</td>
      </tr>
      <tr>
       <td><code>05</code></td>
       <td>BT.470 System B, G; BT.601; BT.1358 625; BT.1700 625 PAL and 625 SECAM</td>
      </tr>
      <tr>
       <td><code>06</code></td>
       <td>BT.601 525; BT.1358 525 or 625; BT.1700 NTSC; SMPTE 170M. <em>Functionally identical to <code>7</code>.</em></td>
      </tr>
      <tr>
       <td><code>70</code></td>
       <td>{{Glossary("SMPTE")}} 240M (historical). <em>Functionally identical to <code>6</code>.</em></td>
      </tr>
      <tr>
       <td><code>08</code></td>
       <td>Generic film</td>
      </tr>
      <tr>
       <td><code>09</code></td>
       <td>BT.2020; BT.2100. Used for ultra-high definition (4K) High Dynamic Range (HDR) video, these have a very wide color gamut and support 10-bit and 12-bit color component depths.</td>
      </tr>
      <tr>
       <td><code>10</code></td>
       <td>SMPTE ST 428 (D-Cinema Distribution Master: Image characteristics). Defines the uncompressed image characteristics for DCDM.</td>
      </tr>
      <tr>
       <td><code>11</code></td>
       <td>SMPTE RP 431 (D-Cinema Quality: Reference projector and environment). Describes the reference projector and environment conditions that provide a consistent film presentation experience.</td>
      </tr>
      <tr>
       <td><code>12</code></td>
       <td>SMPTE EG 432 (Digital Source Processing: Color Processing for D-Cinema). Engineering guideline making color signal decoding recommendations for digital movies.</td>
      </tr>
      <tr>
       <td><code>13</code> – <code>21</code></td>
       <td><em>Reserved for future use by ITU-T or ISO/IEC</em></td>
      </tr>
      <tr>
       <td><code>22</code></td>
       <td>EBU Tech 3213-E</td>
      </tr>
      <tr>
       <td><code>23</code> – <code>255</code></td>
       <td><em>Reserved for future use by ITU-T or ISO/IEC</em></td>
      </tr>
     </tbody>
    </table>
   </td>
  </tr>
  <tr>
   <td><code>tc</code></td>
   <td>A two-digit integer indicating the <code>transferCharacteristics</code> for the video. This value is from Section 8.2 of <a href="https://www.itu.int/rec/T-REC-H.273/en">ISO/IEC 23001-8:2016</a>, and indicates the transfer characteristics to be used when adapting the decoded color to the render target.</td>
  </tr>
  <tr>
   <td><code>mc</code></td>
   <td>The two-digit value for the <code>matrixCoefficients</code> property. This value comes from the table in Section 8.3 of the <a href="https://www.itu.int/rec/T-REC-H.273/en">ISO/IEC 23001-8:2016</a> specification. This value indicates which set of coefficients to use when mapping from the native red, blue, and green primaries to the luma and chroma signals. These coefficients are in turn used with the equations found in that same section.</td>
  </tr>
  <tr>
   <td><code>FF</code></td>
   <td>Indicates whether to restrict the black level and color range of each color component to the legal range. For 8 bit color samples, the legal range is 16-235. A value of <code>00</code> indicates that these limitations should be enforced, while a value of <code>01</code> allows the full range of possible values for each component, even if the resulting color is out of bounds for the color system.</td>
  </tr>
 </tbody>
</table>

<h4 id="WebM_media_type_examples">WebM media type examples</h4>

<dl>
 <dt><code>video/webm;codecs="vp08.00.41.08,vorbis"</code></dt>
 <dd>VP8 video, profile 0 level 4.1, using 8-bit YUV with 4:2:0 chroma subsampling, using BT.709 color primaries, transfer function, and matrix coefficients, with the luminance and chroma values encoded within the legal ("studio") range. The video is Vorbis.</dd>
 <dt><code>video/webm;codecs="vp09.02.10.10.01.09.16.09.01,opus"</code></dt>
 <dd>VP9 video, profile 2 level 1.0, with 10-bit YUV content using 4:2:0 chroma subsampling, BT.2020 primaries, ST 2084 EOTF (HDR SMPTE), BT.2020 non-constant luminance color matrix, and full-range chroma and luma encoding. The audio is in Opus format.</dd>
</dl>

<h2 id="Using_the_codecs_parameter">Using the codecs parameter</h2>

<p>You can use the <code>codecs</code> parameter in a few situations. Firstly, you can use it with the {{HTMLElement("source")}} element when creating an {{HTMLElement("audio")}} or {{HTMLElement("video")}} element, in order to establish a group of options for the browser to choose from when selecting the format of the media to present to the user in the element.</p>

<p>You can also use the codecs parameter when specifying a MIME media type to the {{domxref("MediaSource.isTypeSupported()")}} method; this method returns a Boolean which indicates whether or not the media is likely to work on the current device.</p>

<h2 id="See_also">See also</h2>

<ul>
 <li><a href="/en-US/docs/Web/Media">Web media technologies</a></li>
 <li><a href="/en-US/docs/Web/Media/Formats">Guide to media types and formats on the web</a></li>
 <li><a href="/en-US/docs/Web/Media/Formats/Audio_codecs">Guide to audio codecs used on the web</a></li>
 <li><a href="/en-US/docs/Web/Media/Formats/Video_codecs">Guide to video codecs used on the web</a></li>
 <li><a href="/en-US/docs/Web/Media/Formats/WebRTC_codecs">Codecs used by WebRTC</a></li>
</ul>