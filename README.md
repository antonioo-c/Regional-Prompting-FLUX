<div align="center">
<h1>Training-free Regional Prompting for Diffusion Transformers</h1>

[**Anthony Chen**](https://atchen.com/)<sup>1,2</sup> · [**Jianjin Xu**](#)<sup>3</sup> · [**Wenzhao Zheng**](#)<sup>4</sup> · [**Gaole Dai**](#)<sup>1</sup> · [**Yida Wang**](#)<sup>5</sup> · [**Renrui Zhang**](#)<sup>6</sup> · [**Haofan Wang**](https://haofanwang.github.io/)<sup>2</sup> · [**Shanghang Zhang**](#)<sup>1*</sup>

<sup>1</sup>Peking University · <sup>2</sup>InstantX Team · <sup>3</sup>Carnegie Mellon University · <sup>4</sup>UC Berkeley · <sup>5</sup>Li Auto Inc. · <sup>6</sup>CUHK

<a href='https://arxiv.org/abs/2411.02395'><img src='https://img.shields.io/badge/Technique-Report-red'></a>

</div>

Training-free Regional Prompting for Diffusion Transformers(Regional-Prompting-FLUX) enables Diffusion Transformers (i.e., FLUX) with find-grained compositional text-to-image generation capability in a training-free manner. Empirically, we show that our method is highly effective and compatible with LoRA and ControlNet.

<!-- <img src='assets/pipe.png'> -->

<div align="center">
<img src='assets/demo_pipeline.png' width = 900 >
</div>

We inference at speed **much faster** than the [RPG-based](https://github.com/YangLing0818/RPG-DiffusionMaster) implementation, yet take up **less GPU memory**.

<p align="center">
  <img src="assets/demo_speed.png" width = 400>
</p>

## Release
- [2024/11/05] 🔥 We release the code, feel free to try it out!
- [2024/11/05] 🔥 We release the [technical report](https://arxiv.org/abs/2411.02395)!

## Demos

### Custom Regional Control

<table align="center">
  <tr>
    <th>Regional Masks</th>
    <th>Configuration</th>
    <th>Generated Result</th>
  </tr>
  <tr>
    <td width="10%">
      <img src="assets/demo_custom_1_layout.png" width="100%">
      <br>
      <small><i>Red: Cocktail region (xyxy: [450, 560, 960, 900])<br>Green: Table region (xyxy: [320, 900, 1280, 1280])<br>Blue: Background</i></small>
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "A tropical cocktail on a wooden table at a beach during sunset."
      <br><br>
      <b>Background Prompt:</b><br>
      "A photo"
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A colorful cocktail in a glass with tropical fruits and a paper umbrella, with ice cubes and condensation."</li>
        <li><b>Region 1:</b> "Weathered wooden table with seashells and a napkin."</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x1280</li>
        <li>Seed: 124</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Interval: 1</li>
        <li>Single Inject Interval: 2</li>
        <li>Base Ratio: 0.1</li>
      </ul>
    </td>
    <td width="50%">
      <img src="assets/demo_custom_1.jpg" width="100%">
    </td>
  </tr>
  <tr>
    <td width="10%">
      <img src="assets/demo_custom_2_layout.png" width="100%">
      <br>
      <small><i>Red: Rainbow region (xyxy: [0, 0, 1280, 256])<br>Green: Ship region (xyxy: [0, 256, 1280, 520])<br>Yellow: Fish region (xyxy: [0, 520, 640, 768])<br>Blue: Treasure region (xyxy: [640, 520, 1280, 768])</i></small>
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "A majestic ship sails under a rainbow as vibrant marine creatures glide through crystal waters below, embodying nature's wonder, while an ancient, rusty treasure chest lies hidden on the ocean floor."
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A massive, radiant rainbow arches across the vast sky, glowing in vivid colors and blending with ethereal clouds that drift gently, casting a magical light across the scene and creating a surreal, dreamlike atmosphere."</li>
        <li><b>Region 1:</b> "The majestic ship, with grand sails billowing against the crystal blue waters, glides forward as birds soar overhead. Its hull and sails mirror the vivid hues of the sea, embodying a sense of adventure and mystery as it journeys through this enchanted world."</li>
        <li><b>Region 2:</b> "Beneath the sparkling water, schools of colorful fish dart playfully, their scales flashing in shades of yellow, blue, and orange. Tiny seahorses drift by, while gentle turtles paddle along, creating a lively, enchanting underwater scene."</li>
        <li><b>Region 3:</b> "On the ocean floor lies an ancient, rusty treasure chest, heavily encrusted with barnacles and seaweed. The chest's corroded metal and weathered wood hint at centuries spent underwater. Its lid is slightly ajar, revealing a faint glow within, as small fish dart around, adding an air of mystery to the forgotten relic."</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x768</li>
        <li>Seed: 124</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Interval: 1</li>
        <li>Single Inject Interval: 1</li>
        <li>Base Ratio: 0.2</li>
      </ul>
    </td>
    <td width="50%">
      <img src="assets/demo_custom_2.jpg" width="100%">
    </td>
  </tr>
  <tr>
    <td width="10%">
      <img src="assets/demo_custom_3_layout.png" width="100%">
      <br>
      <small><i>Red: Woman with torch region (xyxy: [128, 128, 640, 768])</i></small>
      <br><small><i>Green: Background</i></small>
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "An ancient woman stands solemnly holding a blazing torch, while a fierce battle rages in the background, capturing both strength and tragedy in a historical war scene."
      <br><br>
      <b>Background Prompt:</b><br>
      "A photo."
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A dignified woman in ancient robes stands in the foreground, her face illuminated by the torch she holds high. Her expression is one of determination and sorrow, her clothing and appearance reflecting the historical period. The torch casts dramatic shadows across her features, its flames dancing vibrantly against the darkness."</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x768</li>
        <li>Seed: 124</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Interval: 1</li>
        <li>Single Inject Interval: 1</li>
        <li>Base Ratio: 0.3</li>
      </ul>
    </td>
    <td width="50%">
      <img src="assets/demo_custom_3.jpg" width="100%">
    </td>
  </tr>
  <tr>
    <td width="10%">
      <img src="assets/demo_custom_0_layout.png" width="100%">
      <br>
      <small><i>Red: Dog region (assets/demo_custom_0_mask_0.png)<br>Green: Cat region (assets/demo_custom_0_mask_1.png)<br>Blue: Background</i></small>
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "dog and cat sitting on lush green grass, in a sunny outdoor setting."
      <br><br>
      <b>Background Prompt:</b><br>
      "A photo"
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A friendly golden retriever with a luxurious golden coat, floppy ears, and warm expression sitting on vibrant green grass."</li>
        <li><b>Region 1:</b> "A golden british shorthair cat with round face, plush coat, and copper eyes sitting regally"</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x768</li>
        <li>Seed: 124</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Interval: 1</li>
        <li>Single Inject Interval: 2</li>
        <li>Base Ratio: 0.1</li>
      </ul>
    </td>
    <td width="50%">
      <img src="assets/demo_custom_0.jpg" width="100%">
      <br>
      <small><i>Note: Generation with segmentation mask is a experimental function, the generated image is not perfectly constrained by the regions, we assume it is because the mask suffers from degradation during the downsampling process.</i></small>
    </td>
  </tr>
</table>

### LoRA Compatability

<table align="center">
  <tr>
    <th>Regional Masks</th>
    <th>Configuration</th>
    <th>Generated Result</th>
  </tr>
  <tr>
    <td width="20%">
      <img src="assets/demo_lora_0_layout.png" width="100%">
      <br>
      <small><i>Red: Dinosaur region (xyxy: [0, 0, 640, 1280])</i></small>
      <small><i>Blue: City region (xyxy: [640, 0, 1280, 1280])</i></small>
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "Sketched style: A cute dinosaur playfully blowing tiny fire puffs over a cartoon city in a cheerful scene."
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "Sketched style, dinosaur with round eyes and a mischievous smile, puffing small flames over the city."</li>
        <li><b>Region 1:</b> "Sketched style, city with colorful buildings and tiny flames gently floating above, adding a playful touch."</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x1280</li>
        <li>Seed: 1298</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Interval: 1</li>
        <li>Single Inject Interval: 1</li>
        <li>Base Ratio: 0.1</li>
      </ul>
      <b>LoRA:</b>
      <ul>
        <li>Path: Shakker-Labs/FLUX.1-dev-LoRA-Children-Simple-Sketch</li>
        <li>Scale: 1.5</li>
        <li>Trigger Words: "sketched style"</li>
      </ul>
    </td>
    <td width="40%">
      <img src="assets/demo_lora_0.jpg" width="100%">
    </td>
  </tr>
  <tr>
    <td width="20%">
      <img src="assets/demo_lora_2_layout.png" width="100%">
      <br>
      <small><i>Red: UFO region (xyxy: [320, 320, 640, 640])</i></small>
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "A cute cartoon-style UFO floating above a sunny city street, artistic style blends reality and illustration elements"
      <br><br>
      <b>Background Prompt:</b><br>
      "A photo"
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A cartoon-style silver UFO with blinking lights hovering in the air, artistic style blends reality and illustration elements"</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x1280</li>
        <li>Seed: 1298</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Interval: 1</li>
        <li>Single Inject Interval: 2</li>
        <li>Base Ratio: 0.2</li>
      </ul>
      <b>LoRA:</b>
      <ul>
        <li>Path: Shakker-Labs/FLUX.1-dev-LoRA-Vector-Journey</li>
        <li>Scale: 1.0</li>
      </ul>
    </td>
    <td width="40%">
      <img src="assets/demo_lora_2.jpg" width="100%">
    </td>
  </tr>
</table>

### ControlNet Compatability

<table align="center">
  <tr>
    <th>Regional Masks</th>
    <th>Configuration</th>
    <th>Generated Result</th>
  </tr>
  <tr>
    <td width="20%">
      <img src="assets/demo_controlnet_0_layout.png" width="100%">
      <br>
      <small><i>Red: First car region (xyxy: [0, 0, 426, 968])<br>
      Green: Second car region (xyxy: [426, 0, 853, 968])<br>
      Blue: Third car region (xyxy: [853, 0, 1280, 968])</i></small>
      <br><br>
      <img src="./assets/condition_depth.png" width="100%">
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "Three high-performance sports cars, red, blue, and yellow, are racing side by side on a city street"
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A sleek red sports car in the lead position, with aggressive aerodynamic styling and gleaming paint that catches the light. The car appears to be moving at high speed with motion blur effects."</li>
        <li><b>Region 1:</b> "A powerful blue sports car in the middle position, neck-and-neck with its competitors. Its metallic paint shimmers as it races forward, with visible speed lines and dynamic movement."</li>
        <li><b>Region 2:</b> "A striking yellow sports car in the third position, its bold color standing out against the street. The car's aggressive stance and aerodynamic profile emphasize its racing performance."</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x968</li>
        <li>Seed: 124</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Blocks Interval: 1</li>
        <li>Single Inject Blocks Interval: 2</li>
        <li>Base Ratio: 0.2</li>
      </ul>
      <b>ControlNet:</b>
      <ul>
        <li>Control Mode: 2</li>
        <li>ControlNet Conditioning Scale: 0.7</li>
      </ul>
    </td>
    <td width="40%">
      <img src="assets/demo_controlnet_0.jpg" width="100%">
    </td>
  </tr>
  <tr>
    <td width="20%">
      <img src="assets/demo_controlnet_1_layout.png" width="100%">
      <br>
      <small><i>Red: Woman region (xyxy: [0, 0, 640, 968])<br>
      Green: Beach region (xyxy: [640, 0, 1280, 968])</i></small>
      <br><br>
      <img src="./assets/condition_pose.png" width="100%">
    </td>
    <td width="40%">
      <b>Base Prompt:</b><br>
      "A woman walking along a beautiful beach with a scenic coastal view."
      <br><br>
      <b>Regional Prompts:</b>
      <ul>
        <li><b>Region 0:</b> "A woman in a flowing summer dress with delicate pink and blue flower patterns walking barefoot on the sandy beach. Her floral-patterned dress billows gracefully in the ocean breeze as she strolls casually along the shoreline, with a peaceful expression on her face and her hair gently tousled by the wind."</li>
        <li><b>Region 1:</b> "A stunning coastal landscape with crystal clear turquoise waters meeting the horizon. Rhythmic waves roll in with white foamy crests, creating a mesmerizing pattern as they crash onto the shore. The waves vary in size, some gently lapping at the sand while others surge forward with more force. White sandy beach stretches into the distance, with gentle waves leaving intricate patterns on the wet sand and scattered palm trees swaying in the breeze."</li>
      </ul>
      <b>Settings:</b>
      <ul>
        <li>Image Size: 1280x968</li>
        <li>Seed: 124</li>
        <li>Mask Inject Steps: 10</li>
        <li>Double Inject Blocks Interval: 1</li>
        <li>Single Inject Blocks Interval: 2</li>
        <li>Base Ratio: 0.2</li>
      </ul>
      <b>ControlNet:</b>
      <ul>
        <li>Control Mode: 4</li>
        <li>ControlNet Conditioning Scale: 0.7</li>
      </ul>
    </td>
    <td width="40%">
      <img src="assets/demo_controlnet_1.jpg" width="100%">
    </td>
  </tr>
</table>

## Installation
We use previous commit from diffusers repo to ensure reproducibility, as we found new diffusers version may experience different results.
```
# install diffusers locally
git clone https://github.com/huggingface/diffusers.git
cd diffusers

# reset diffusers version to 0.31.dev, where we developed Regional-Prompting-FLUX on, different version may experience different results
git reset --hard d13b0d63c0208f2c4c078c4261caf8bf587beb3b
pip install -e ".[torch]"
cd ..

# install other dependencies
pip install -U transformers sentencepiece protobuf PEFT

# clone this repo
git clone https://github.com/antonioo-c/Regional-Prompting-FLUX.git

# replace file in diffusers
cd Regional-Prompting-FLUX
cp transformer_flux.py ../diffusers/src/diffusers/models/transformers/transformer_flux.py
```

## Quick Start
See detailed example (including LoRAs and ControlNets) in [infer_flux_regional.py](infer_flux_regional.py). Below is a quick start example.

```python
import torch
from pipeline_flux_regional import RegionalFluxPipeline, RegionalFluxAttnProcessor2_0

pipeline = RegionalFluxPipeline.from_pretrained("black-forest-labs/FLUX.1-dev", torch_dtype=torch.bfloat16).to("cuda")
attn_procs = {}
for name in pipeline.transformer.attn_processors.keys():
    if 'transformer_blocks' in name and name.endswith("attn.processor"):
        attn_procs[name] = RegionalFluxAttnProcessor2_0()
    else:
        attn_procs[name] = pipeline.transformer.attn_processors[name]
pipeline.transformer.set_attn_processor(attn_procs)

## general settings
image_width = 1280
image_height = 768
num_inference_steps = 24
seed = 124
base_prompt = "An ancient woman stands solemnly holding a blazing torch, while a fierce battle rages in the background, capturing both strength and tragedy in a historical war scene."
background_prompt = "a photo" # set by default, but if you want to enrich background, you can set it to a more descriptive prompt
regional_prompt_mask_pairs = {
    "0": {
        "description": "A dignified woman in ancient robes stands in the foreground, her face illuminated by the torch she holds high. Her expression is one of determination and sorrow, her clothing and appearance reflecting the historical period. The torch casts dramatic shadows across her features, its flames dancing vibrantly against the darkness.",
        "mask": [128, 128, 640, 768]
    }
}
## region control factor settings
mask_inject_steps = 10 # larger means stronger control, recommended between 5-10
double_inject_blocks_interval = 1 # 1 means strongest control
single_inject_blocks_interval = 1 # 1 means strongest control
base_ratio = 0.2 # smaller means stronger control

regional_prompts = []
regional_masks = []
background_mask = torch.ones((image_height, image_width))
for region_idx, region in regional_prompt_mask_pairs.items():
    description = region['description']
    mask = region['mask']
    x1, y1, x2, y2 = mask
    mask = torch.zeros((image_height, image_width))
    mask[y1:y2, x1:x2] = 1.0
    background_mask -= mask
    regional_prompts.append(description)
    regional_masks.append(mask)
# if regional masks don't cover the whole image, append background prompt and mask
if background_mask.sum() > 0:
    regional_prompts.append(background_prompt)
    regional_masks.append(background_mask)

image = pipeline(
    prompt=base_prompt,
    width=image_width, height=image_height,
    mask_inject_steps=mask_inject_steps,
    num_inference_steps=num_inference_steps,
    generator=torch.Generator("cuda").manual_seed(seed),
    joint_attention_kwargs={
        "regional_prompts": regional_prompts,
        "regional_masks": regional_masks,
        "double_inject_blocks_interval": double_inject_blocks_interval,
        "single_inject_blocks_interval": single_inject_blocks_interval,
        "base_ratio": base_ratio
    },
  ).images[0]

image.save(f"output.jpg")
```

## 👏 Acknowledgment
Our work is sponsored by [HuggingFace](https://huggingface.co) and [fal.ai](https://fal.ai). Thanks!

## Cite
If you find Regional-Prompting-FLUX useful for your research and applications, please cite us using this BibTeX:

```bibtex
@article{chen2024training,
  title={Training-free Regional Prompting for Diffusion Transformers},
  author={Chen, Anthony and Xu, Jianjin and Zheng, Wenzhao and Dai, Gaole and Wang, Yida and Zhang, Renrui and Wang, Haofan and Zhang, Shanghang},
  journal={arXiv preprint arXiv:2411.02395},
  year={2024}
}
```

For any question, feel free to contact us via antonchen@pku.edu.cn.
