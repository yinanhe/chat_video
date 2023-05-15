---
title: 'VideoChat: Chat-Centric Video Understanding'
emoji: 👀
colorFrom: green
colorTo: blue
sdk: gradio
python_version: 3.8.16
app_file: app.py
pinned: false
license: mit
---

# 🦜 VideoChat [[paper](https://arxiv.org/abs/2305.06355)]

![images](assert/framework.png)
In this study, we initiate an exploration into video understanding by introducing VideoChat, an **end-to-end chat-centric video understanding system**. It integrates video foundation models and large language models via a learnable neural interface, excelling in **spatiotemporal reasoning, event localization, and causal relationship inference**. To instructively tune this system, we propose a **video-centric instruction dataset**, composed of thousands of videos matched with detailed descriptions and conversations. This dataset emphasizes **spatiotemporal reasoning and causal relationships**, providing a valuable asset for training chat-centric video understanding systems. Preliminary qualitative experiments reveal our system’s potential across a broad spectrum of video applications and set the standard for future research.


# :fire: Updates
- **2023/05/11**: Release the 🦜**VideoChat V1**, which can **handle both image and video understanding!**
    - [Model](https://drive.google.com/file/d/1BqmWHWCZBPkhTNWDAq0IfGpbkKLz9C0V/view?usp=share_link) and [Data](https://github.com/OpenGVLab/InternVideo/blob/main/Data/instruction_data.md).
    - 🧑‍💻 *Online demo is Preparing*.
    - 🧑‍🔧 *Tuning scripts are cleaning*.

# :hourglass_flowing_sand: Schedule

- [x] Small-scale video instuction data and tuning
- [x] Instruction tuning on BLIP+UniFormerV2+Vicuna
- [ ] Large-scale and complex video instuction data
- [ ] Instruction tuning on strong video foundation model
- [ ] User-friendly interactions with longer videos
- [ ] ...

# :speech_balloon: Example

<div align="center">
<b>
  <font size="4">Comparison with ChatGPT, MiniGPT-4, LLaVA and mPLUG-Owl. </font>
  <br>
  <font size="4" color="red">Our VideoChat can handle both image and video understanding well!</font>
</b>
</div>
<div align="center">
<img src="assert/comparison.png" width="90%">
</div>

<div align="center">
  <font size="4">
	<a href="https://pjlab-gvm-data.oss-cn-shanghai.aliyuncs.com/papers/media/jesse_dance.mp4">[Video]</a> <b>Why the video is funny?</b>
  </font>
</div>
<div align="center">
<img src="assert/humor.png" width="50%">
</div>

<div align="center">
  <font size="4">
	<a href="https://pjlab-gvm-data.oss-cn-shanghai.aliyuncs.com/papers/media/jp_dance.mp4">[Video]</a> <b>Spatial perception</b>
  </font>
</div>
<div align="center">
<img src="assert/spatial.png" width="50%">
</div>

<div align="center">
  <font size="4">
	<a href="https://pjlab-gvm-data.oss-cn-shanghai.aliyuncs.com/papers/media/car_accident.mp4">[Video]</a> <b>Temporal perception</b>
  </font>
</div>
<div align="center">
<img src="assert/temporal.png" width="50%">
</div>

<div align="center">
  <font size="4">
	<a href="https://pjlab-gvm-data.oss-cn-shanghai.aliyuncs.com/papers/media/idol_dancing.mp4">[Video]</a> <b>Multi-turn conversation</b>
  </font>
</div>
<div align="center">
<img src="assert/multi_turn.png" width="50%">
</div>

<div align="center">
  <font size="4">
	<b>Image understanding</b>
  </font>
</div>
<div align="center">
<img src="assert/image.png" width="100%">
</div>

# :running: Usage

- Prepare the envirment.
    ```shell
    pip install -r requirements.txt
    ```
    
- Download [BLIP2](https://huggingface.co/docs/transformers/main/model_doc/blip-2) model:
    - ViT: `wget https://storage.googleapis.com/sfr-vision-language-research/LAVIS/models/BLIP2/eva_vit_g.pth`
    - QFormer: `wget https://storage.googleapis.com/sfr-vision-language-research/LAVIS/models/BLIP2/blip2_pretrained_flant5xxl.pth`
    - Change the `vit_model_path` and `q_former_model_path` in [config.json](./configs/config.json).
    
- Download [StabelVicuna](https://huggingface.co/CarperAI/stable-vicuna-13b-delta) model:
    - LLAMA: Download it from the [original repo](https://github.com/facebookresearch/llama) or [hugging face](https://huggingface.co/decapoda-research/llama-13b-hf).
    - If you download LLAMA from the original repo, please process it via the following command:
    ```shell
    # convert_llama_weights_to_hf is copied from transformers
    python src/transformers/models/llama/convert_llama_weights_to_hf.py \
      --input_dir /path/to/downloaded/llama/weights \
      --model_size 7B --output_dir /output/path
    ```
    - Download [StableVicuna-13b-deelta](https://huggingface.co/CarperAI/stable-vicuna-13b-delta) and process it:
    ```shell
    # fastchat v0.1.10
    python3 apply_delta.py \
      --base /path/to/model_weights/llama-13b \
      --target stable-vicuna-13b \
      --delta CarperAI/stable-vicuna-13b-delta
    ```
    - Change the `llama_model_path` in [config.json](./configs/config.json).
    
- Download [VideoChat](https://drive.google.com/file/d/1BqmWHWCZBPkhTNWDAq0IfGpbkKLz9C0V/view?usp=share_link) model:
  
    - Change the `videochat_model_path` in [config.json](./configs/config.json).
    
- Running demo with Gradio:
    ```shell
    python demo.py
    ```
    
- Another demo on Jupyter Notebook can found in [demo.ipynb](demo.ipynb)


# :page_facing_up: Citation

If you find this project useful in your research, please consider cite:
```BibTeX
@article{2023videochat,
  title={VideoChat: Chat-Centric Video Understanding},
  author={KunChang Li, Yinan He, Yi Wang, Yizhuo Li, Wenhai Wang, Ping Luo, Yali Wang, Limin Wang, and Yu Qiao},
  journal={arXiv preprint arXiv:2305.06355},
  year={2023}
}
```

# :thumbsup: Acknowledgement

Thanks to the open source of the following projects:

[InternVideo](https://github.com/OpenGVLab/InternVideo), [UniFormerV2](https://github.com/OpenGVLab/UniFormerV2), [MiniGPT-4](https://github.com/Vision-CAIR/MiniGPT-4), [LLaVA](https://github.com/haotian-liu/LLaVA), [BLIP2](https://huggingface.co/docs/transformers/main/model_doc/blip-2), [StableLM](https://github.com/Stability-AI/StableLM).