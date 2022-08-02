<template>
  <div class="btn-container_foreground" :style="cssVariables">
    <div class="btn-container">
      <div
        v-for="(button, index) in localOptions"
        v-if="button.id === 1"
        :key="`label-${index}`"
        :class="{
          [`btn-item-${index} labels`]: true,
          ['checked']: button.isActive,
          ['unchecked']: !button.isActive
        }"
        @click="handleLabelClick(button)"
      >
        <div class="active-label">
          <div v-if="button.badge" class="btn-badge">
            {{ button.badge }}
          </div>
          <slot name="icon" :props="button">
            <i :class="`${button.icon}`" />
          </slot>
          <slot v-if="button.icon === 'riwayat'" name="icon" :props="button">
            <svg fill="#ffffff" width="16px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C201.7 512 151.2 495 109.7 466.1C95.2 455.1 91.64 436 101.8 421.5C111.9 407 131.8 403.5 146.3 413.6C177.4 435.3 215.2 448 256 448C362 448 448 362 448 256C448 149.1 362 64 256 64C202.1 64 155 85.46 120.2 120.2L151 151C166.1 166.1 155.4 192 134.1 192H24C10.75 192 0 181.3 0 168V57.94C0 36.56 25.85 25.85 40.97 40.97L74.98 74.98C121.3 28.69 185.3 0 255.1 0L256 0zM256 128C269.3 128 280 138.7 280 152V246.1L344.1 311C354.3 320.4 354.3 335.6 344.1 344.1C335.6 354.3 320.4 354.3 311 344.1L239 272.1C234.5 268.5 232 262.4 232 256V152C232 138.7 242.7 128 256 128V128z"/></svg>
          </slot>
        </div>

        <div class="btn-title">
          <slot name="title" :props="button">
            {{ button.title }}
          </slot>
        </div>

        <div
          v-if="hasChild(button)"
          :class="{
            ['btn-super-parent']: button.isActive,
            ['btn-class-showable']: showable
          }"
        >
          <div class="btn-child-parent">
            <div
              v-for="(child, idx) in button.childs || []"
              :key="idx"
              class="btn-child"
              @click.stop="handleChildClick(child)"
            >
              <slot name="child-icon" :props="child">
                <i :class="`${child.icon}`" />
              </slot>

              <slot v-if="child.icon === 'sakit'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M608 359.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 359.1 608 359.1zM477.2 275c-21-47.13-48.49-151.8-73.11-186.8C365.6 33.63 302.5 0 234.1 0L192 0C86 0 0 86 0 192c0 56.75 24.75 107.6 64 142.9L64 512h223.1v-32h64.01c35.38 0 64-28.62 64-63.1L320 416c-17.67 0-32-14.33-32-32s14.33-32 32-32h95.98l-.003-32h31.99C471.1 320 486.6 296.1 477.2 275zM336 224c-17.62 0-32-14.38-32-32s14.38-32 32-32s32 14.38 32 32S353.6 224 336 224zM480 359.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S493.3 359.1 480 359.1zM608 311.1c13.25 0 24-10.75 24-24s-10.75-24-24-24s-24 10.75-24 24S594.8 311.1 608 311.1zM544 311.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 311.1 544 311.1zM544 407.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 407.1 544 407.1zM608 455.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 455.1 608 455.1z"/></svg>
              </slot>

              <slot v-if="child.icon === 'izin'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M640 320V368C640 385.7 625.7 400 608 400H574.7C567.1 445.4 527.6 480 480 480C432.4 480 392.9 445.4 385.3 400H254.7C247.1 445.4 207.6 480 160 480C112.4 480 72.94 445.4 65.33 400H32C14.33 400 0 385.7 0 368V256C0 228.9 16.81 205.8 40.56 196.4L82.2 92.35C96.78 55.9 132.1 32 171.3 32H353.2C382.4 32 409.1 45.26 428.2 68.03L528.2 193C591.2 200.1 640 254.8 640 319.1V320zM171.3 96C158.2 96 146.5 103.1 141.6 116.1L111.3 192H224V96H171.3zM272 192H445.4L378.2 108C372.2 100.4 362.1 96 353.2 96H272V192zM525.3 400C527 394.1 528 389.6 528 384C528 357.5 506.5 336 480 336C453.5 336 432 357.5 432 384C432 389.6 432.1 394.1 434.7 400C441.3 418.6 459.1 432 480 432C500.9 432 518.7 418.6 525.3 400zM205.3 400C207 394.1 208 389.6 208 384C208 357.5 186.5 336 160 336C133.5 336 112 357.5 112 384C112 389.6 112.1 394.1 114.7 400C121.3 418.6 139.1 432 160 432C180.9 432 198.7 418.6 205.3 400z"/></svg>
              </slot>

              <span class="btn-child-title">
                <slot name="child-title" :props="child">
                  {{ child.title }}
                </slot>
              </span>

              <div v-if="child.badge" class="btn-child-badge">
                {{ child.badge }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <div
        v-for="(button, index) in localOptions"
        v-if="button.id === 2"
        :key="`label-${index}`"
        :class="{
          [`btn-item-${index} labels`]: true,
          ['checked']: button.isActive,
          ['unchecked']: !button.isActive
        }"
        @click="handleLabelClick(button)"
      >
        <div class="active-label">
          <div v-if="button.badge" class="btn-badge">
            {{ button.badge }}
          </div>
          <slot name="icon" :props="button">
            <i :class="`${button.icon}`" />
          </slot>
          <slot v-if="button.icon === 'riwayat'" name="icon" :props="button">
            <svg fill="#ffffff" width="16px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C201.7 512 151.2 495 109.7 466.1C95.2 455.1 91.64 436 101.8 421.5C111.9 407 131.8 403.5 146.3 413.6C177.4 435.3 215.2 448 256 448C362 448 448 362 448 256C448 149.1 362 64 256 64C202.1 64 155 85.46 120.2 120.2L151 151C166.1 166.1 155.4 192 134.1 192H24C10.75 192 0 181.3 0 168V57.94C0 36.56 25.85 25.85 40.97 40.97L74.98 74.98C121.3 28.69 185.3 0 255.1 0L256 0zM256 128C269.3 128 280 138.7 280 152V246.1L344.1 311C354.3 320.4 354.3 335.6 344.1 344.1C335.6 354.3 320.4 354.3 311 344.1L239 272.1C234.5 268.5 232 262.4 232 256V152C232 138.7 242.7 128 256 128V128z"/></svg>
          </slot>
        </div>

        <div class="btn-title">
          <slot name="title" :props="button">
            {{ button.title }}
          </slot>
        </div>

        <div
          v-if="hasChild(button)"
          :class="{
            ['btn-super-parent']: button.isActive,
            ['btn-class-showable']: showable
          }"
        >
          <div class="btn-child-parent">
            <div
              v-for="(child, idx) in button.childs || []"
              :key="idx"
              class="btn-child"
              @click.stop="handleChildClick(child)"
            >
              <slot name="child-icon" :props="child">
                <i :class="`${child.icon}`" />
              </slot>

              <slot v-if="child.icon === 'sakit'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M608 359.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 359.1 608 359.1zM477.2 275c-21-47.13-48.49-151.8-73.11-186.8C365.6 33.63 302.5 0 234.1 0L192 0C86 0 0 86 0 192c0 56.75 24.75 107.6 64 142.9L64 512h223.1v-32h64.01c35.38 0 64-28.62 64-63.1L320 416c-17.67 0-32-14.33-32-32s14.33-32 32-32h95.98l-.003-32h31.99C471.1 320 486.6 296.1 477.2 275zM336 224c-17.62 0-32-14.38-32-32s14.38-32 32-32s32 14.38 32 32S353.6 224 336 224zM480 359.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S493.3 359.1 480 359.1zM608 311.1c13.25 0 24-10.75 24-24s-10.75-24-24-24s-24 10.75-24 24S594.8 311.1 608 311.1zM544 311.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 311.1 544 311.1zM544 407.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 407.1 544 407.1zM608 455.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 455.1 608 455.1z"/></svg>
              </slot>

              <slot v-if="child.icon === 'izin'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M640 320V368C640 385.7 625.7 400 608 400H574.7C567.1 445.4 527.6 480 480 480C432.4 480 392.9 445.4 385.3 400H254.7C247.1 445.4 207.6 480 160 480C112.4 480 72.94 445.4 65.33 400H32C14.33 400 0 385.7 0 368V256C0 228.9 16.81 205.8 40.56 196.4L82.2 92.35C96.78 55.9 132.1 32 171.3 32H353.2C382.4 32 409.1 45.26 428.2 68.03L528.2 193C591.2 200.1 640 254.8 640 319.1V320zM171.3 96C158.2 96 146.5 103.1 141.6 116.1L111.3 192H224V96H171.3zM272 192H445.4L378.2 108C372.2 100.4 362.1 96 353.2 96H272V192zM525.3 400C527 394.1 528 389.6 528 384C528 357.5 506.5 336 480 336C453.5 336 432 357.5 432 384C432 389.6 432.1 394.1 434.7 400C441.3 418.6 459.1 432 480 432C500.9 432 518.7 418.6 525.3 400zM205.3 400C207 394.1 208 389.6 208 384C208 357.5 186.5 336 160 336C133.5 336 112 357.5 112 384C112 389.6 112.1 394.1 114.7 400C121.3 418.6 139.1 432 160 432C180.9 432 198.7 418.6 205.3 400z"/></svg>
              </slot>

              <span class="btn-child-title">
                <slot name="child-title" :props="child">
                  {{ child.title }}
                </slot>
              </span>

              <div v-if="child.badge" class="btn-child-badge">
                {{ child.badge }}
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <div
        v-for="(button, index) in localOptions"
        v-if="button.id === 3"
        :key="`label-${index}`"
        class="btn-item-2 labels checked"
        @click="handleLabelClick(button)"
      >
        <div class="active-label">
          <div v-if="button.badge" class="btn-badge">
            {{ button.badge }}
          </div>
          <slot name="icon" :props="button">
            <i :class="`${button.icon}`" />
          </slot>
          <slot v-if="button.icon === 'riwayat'" name="icon" :props="button">
            <svg fill="#ffffff" width="16px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C201.7 512 151.2 495 109.7 466.1C95.2 455.1 91.64 436 101.8 421.5C111.9 407 131.8 403.5 146.3 413.6C177.4 435.3 215.2 448 256 448C362 448 448 362 448 256C448 149.1 362 64 256 64C202.1 64 155 85.46 120.2 120.2L151 151C166.1 166.1 155.4 192 134.1 192H24C10.75 192 0 181.3 0 168V57.94C0 36.56 25.85 25.85 40.97 40.97L74.98 74.98C121.3 28.69 185.3 0 255.1 0L256 0zM256 128C269.3 128 280 138.7 280 152V246.1L344.1 311C354.3 320.4 354.3 335.6 344.1 344.1C335.6 354.3 320.4 354.3 311 344.1L239 272.1C234.5 268.5 232 262.4 232 256V152C232 138.7 242.7 128 256 128V128z"/></svg>
          </slot>
        </div>

        <div class="btn-title">
          <slot name="title" :props="button">
            {{ button.title }}
          </slot>
        </div>
      </div>

      <div
        v-for="(button, index) in localOptions"
        v-if="button.id === 4"
        :key="`label-${index}`"
        :class="{
          [`btn-item-${index} labels`]: true,
          ['checked']: button.isActive,
          ['unchecked']: !button.isActive
        }"
        @click="handleLabelClick(button)"
      >
        <div class="active-label">
          <div v-if="button.badge" class="btn-badge">
            {{ button.badge }}
          </div>
          <slot name="icon" :props="button">
            <i :class="`${button.icon}`" />
          </slot>
          <slot v-if="button.icon === 'riwayat'" name="icon" :props="button">
            <svg fill="#ffffff" width="16px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C201.7 512 151.2 495 109.7 466.1C95.2 455.1 91.64 436 101.8 421.5C111.9 407 131.8 403.5 146.3 413.6C177.4 435.3 215.2 448 256 448C362 448 448 362 448 256C448 149.1 362 64 256 64C202.1 64 155 85.46 120.2 120.2L151 151C166.1 166.1 155.4 192 134.1 192H24C10.75 192 0 181.3 0 168V57.94C0 36.56 25.85 25.85 40.97 40.97L74.98 74.98C121.3 28.69 185.3 0 255.1 0L256 0zM256 128C269.3 128 280 138.7 280 152V246.1L344.1 311C354.3 320.4 354.3 335.6 344.1 344.1C335.6 354.3 320.4 354.3 311 344.1L239 272.1C234.5 268.5 232 262.4 232 256V152C232 138.7 242.7 128 256 128V128z"/></svg>
          </slot>
        </div>

        <div class="btn-title">
          <slot name="title" :props="button">
            {{ button.title }}
          </slot>
        </div>

        <div
          v-if="hasChild(button)"
          :class="{
            ['btn-super-parent']: button.isActive,
            ['btn-class-showable']: showable
          }"
        >
          <div class="btn-child-parent">
            <div
              v-for="(child, idx) in button.childs || []"
              :key="idx"
              class="btn-child"
              @click.stop="handleChildClick(child)"
            >
              <slot name="child-icon" :props="child">
                <i :class="`${child.icon}`" />
              </slot>

              <slot v-if="child.icon === 'sakit'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M608 359.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 359.1 608 359.1zM477.2 275c-21-47.13-48.49-151.8-73.11-186.8C365.6 33.63 302.5 0 234.1 0L192 0C86 0 0 86 0 192c0 56.75 24.75 107.6 64 142.9L64 512h223.1v-32h64.01c35.38 0 64-28.62 64-63.1L320 416c-17.67 0-32-14.33-32-32s14.33-32 32-32h95.98l-.003-32h31.99C471.1 320 486.6 296.1 477.2 275zM336 224c-17.62 0-32-14.38-32-32s14.38-32 32-32s32 14.38 32 32S353.6 224 336 224zM480 359.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S493.3 359.1 480 359.1zM608 311.1c13.25 0 24-10.75 24-24s-10.75-24-24-24s-24 10.75-24 24S594.8 311.1 608 311.1zM544 311.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 311.1 544 311.1zM544 407.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 407.1 544 407.1zM608 455.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 455.1 608 455.1z"/></svg>
              </slot>

              <slot v-if="child.icon === 'izin'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M640 320V368C640 385.7 625.7 400 608 400H574.7C567.1 445.4 527.6 480 480 480C432.4 480 392.9 445.4 385.3 400H254.7C247.1 445.4 207.6 480 160 480C112.4 480 72.94 445.4 65.33 400H32C14.33 400 0 385.7 0 368V256C0 228.9 16.81 205.8 40.56 196.4L82.2 92.35C96.78 55.9 132.1 32 171.3 32H353.2C382.4 32 409.1 45.26 428.2 68.03L528.2 193C591.2 200.1 640 254.8 640 319.1V320zM171.3 96C158.2 96 146.5 103.1 141.6 116.1L111.3 192H224V96H171.3zM272 192H445.4L378.2 108C372.2 100.4 362.1 96 353.2 96H272V192zM525.3 400C527 394.1 528 389.6 528 384C528 357.5 506.5 336 480 336C453.5 336 432 357.5 432 384C432 389.6 432.1 394.1 434.7 400C441.3 418.6 459.1 432 480 432C500.9 432 518.7 418.6 525.3 400zM205.3 400C207 394.1 208 389.6 208 384C208 357.5 186.5 336 160 336C133.5 336 112 357.5 112 384C112 389.6 112.1 394.1 114.7 400C121.3 418.6 139.1 432 160 432C180.9 432 198.7 418.6 205.3 400z"/></svg>
              </slot>

              <span class="btn-child-title">
                <slot name="child-title" :props="child">
                  {{ child.title }}
                </slot>
              </span>

              <div v-if="child.badge" class="btn-child-badge">
                {{ child.badge }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <div
        v-for="(button, index) in localOptions"
        v-if="button.id === 5"
        :key="`label-${index}`"
        :class="{
          [`btn-item-${index} labels`]: true,
          ['checked']: button.isActive,
          ['unchecked']: !button.isActive
        }"
        @click="handleLabelClick(button)"
      >
        <div class="active-label">
          <div v-if="button.badge" class="btn-badge">
            {{ button.badge }}
          </div>
          <slot name="icon" :props="button">
            <i :class="`${button.icon}`" />
          </slot>
          <slot v-if="button.icon === 'riwayat'" name="icon" :props="button">
            <svg fill="#ffffff" width="16px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M256 0C397.4 0 512 114.6 512 256C512 397.4 397.4 512 256 512C201.7 512 151.2 495 109.7 466.1C95.2 455.1 91.64 436 101.8 421.5C111.9 407 131.8 403.5 146.3 413.6C177.4 435.3 215.2 448 256 448C362 448 448 362 448 256C448 149.1 362 64 256 64C202.1 64 155 85.46 120.2 120.2L151 151C166.1 166.1 155.4 192 134.1 192H24C10.75 192 0 181.3 0 168V57.94C0 36.56 25.85 25.85 40.97 40.97L74.98 74.98C121.3 28.69 185.3 0 255.1 0L256 0zM256 128C269.3 128 280 138.7 280 152V246.1L344.1 311C354.3 320.4 354.3 335.6 344.1 344.1C335.6 354.3 320.4 354.3 311 344.1L239 272.1C234.5 268.5 232 262.4 232 256V152C232 138.7 242.7 128 256 128V128z"/></svg>
          </slot>
        </div>

        <div class="btn-title">
          <slot name="title" :props="button">
            {{ button.title }}
          </slot>
        </div>

        <div
          v-if="hasChild(button)"
          :class="{
            ['btn-super-parent']: button.isActive,
            ['btn-class-showable']: showable
          }"
        >
          <div class="btn-child-parent">
            <div
              v-for="(child, idx) in button.childs || []"
              :key="idx"
              class="btn-child"
              @click.stop="handleChildClick(child)"
            >
              <slot name="child-icon" :props="child">
                <i :class="`${child.icon}`" />
              </slot>

              <slot v-if="child.icon === 'sakit'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M608 359.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 359.1 608 359.1zM477.2 275c-21-47.13-48.49-151.8-73.11-186.8C365.6 33.63 302.5 0 234.1 0L192 0C86 0 0 86 0 192c0 56.75 24.75 107.6 64 142.9L64 512h223.1v-32h64.01c35.38 0 64-28.62 64-63.1L320 416c-17.67 0-32-14.33-32-32s14.33-32 32-32h95.98l-.003-32h31.99C471.1 320 486.6 296.1 477.2 275zM336 224c-17.62 0-32-14.38-32-32s14.38-32 32-32s32 14.38 32 32S353.6 224 336 224zM480 359.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S493.3 359.1 480 359.1zM608 311.1c13.25 0 24-10.75 24-24s-10.75-24-24-24s-24 10.75-24 24S594.8 311.1 608 311.1zM544 311.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 311.1 544 311.1zM544 407.1c-13.25 0-23.1 10.75-23.1 24s10.75 24 23.1 24s24-10.75 24-24S557.3 407.1 544 407.1zM608 455.1c-13.25 0-24 10.75-24 24s10.75 24 24 24s24-10.75 24-24S621.3 455.1 608 455.1z"/></svg>
              </slot>

              <slot v-if="child.icon === 'izin'" name="child-icon" :props="child">
                <svg fill="#ffffff" width="18px" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 640 512"><!--! Font Awesome Pro 6.1.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. --><path d="M640 320V368C640 385.7 625.7 400 608 400H574.7C567.1 445.4 527.6 480 480 480C432.4 480 392.9 445.4 385.3 400H254.7C247.1 445.4 207.6 480 160 480C112.4 480 72.94 445.4 65.33 400H32C14.33 400 0 385.7 0 368V256C0 228.9 16.81 205.8 40.56 196.4L82.2 92.35C96.78 55.9 132.1 32 171.3 32H353.2C382.4 32 409.1 45.26 428.2 68.03L528.2 193C591.2 200.1 640 254.8 640 319.1V320zM171.3 96C158.2 96 146.5 103.1 141.6 116.1L111.3 192H224V96H171.3zM272 192H445.4L378.2 108C372.2 100.4 362.1 96 353.2 96H272V192zM525.3 400C527 394.1 528 389.6 528 384C528 357.5 506.5 336 480 336C453.5 336 432 357.5 432 384C432 389.6 432.1 394.1 434.7 400C441.3 418.6 459.1 432 480 432C500.9 432 518.7 418.6 525.3 400zM205.3 400C207 394.1 208 389.6 208 384C208 357.5 186.5 336 160 336C133.5 336 112 357.5 112 384C112 389.6 112.1 394.1 114.7 400C121.3 418.6 139.1 432 160 432C180.9 432 198.7 418.6 205.3 400z"/></svg>
              </slot>

              <span class="btn-child-title">
                <slot name="child-title" :props="child">
                  {{ child.title }}
                </slot>
              </span>

              <div v-if="child.badge" class="btn-child-badge">
                {{ child.badge }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <div v-show="hasActiveClass" id="sweep">
        <div id="sweep-right" />
        <div id="sweep-center" />
        <div id="sweep-left" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'VueBottomNavigation',
  model: {
    prop: 'value',
    event: 'update'
  },
  props: {
    value: {
      default: null
    },
    options: {
      type: Array,
      default: () => []
    },
    foregroundColor: {
      type: String,
      default: '#42A5F5'
    },
    backgroundColor: {
      type: String,
      default: '#FFFFFF'
    },
    iconColor: {
      type: String,
      default: '#0000008A'
    },
    badgeColor: {
      type: String,
      default: '#FBC02D'
    },
    replaceRoute: {
      type: Boolean,
      default: false
    }
  },
  data: () => ({
    localOptions: [],
    showable: false,
    enableWatch: true
  }),
  computed: {
    cssVariables() {
      const countChilds = (
        (this.localOptions.find((option) => option.isActive) || {}).childs || []
      ).length;

      const styles = {
        '--color-foreground': this.foregroundColor,
        '--color-background': this.backgroundColor,
        '--color-icon': this.iconColor,
        '--color-badge': this.badgeColor,
        '--width-parent': `${countChilds * 45}px`
      };

      return styles;
    },

    hasActiveClass() {
      return this.localOptions.some((option) => option.isActive);
    }
  },
  watch: {
    options: {
      deep: true,
      handler(newVal) {
        if (newVal) {
          this.localOptions = newVal.map((option) => ({
            ...option,
            isActive: this.isActive(option)
          }));
          this.cssLoader();
        }
      }
    },
    value: {
      handler(newVal, oldVal) {
        if (newVal != oldVal && this.enableWatch) {
          const childs = [];
          this.localOptions.forEach((option) => {
            if (option.childs) {
              childs.push(...option.childs);
            }
          });
          const target = [...this.localOptions, ...childs].find(
            (option) => option.id == newVal
          );
          if (target) {
            this.updateValue(target, this.hasChild(target));
          }
        }
      }
    }
  },
  created() {
    this.localOptions = this.options.map((option) => ({
      ...option,
      isActive: this.isActive(option)
    }));
  },
  mounted() {
    this.cssLoader();
    window.addEventListener('resize', this.onResize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.onResize);
  },
  methods: {
    cssLoader() {
      let customStyle = '';
      const containerWidth =
        document.querySelector('.btn-container').offsetWidth ||
        window.innerWidth;

      this.options.forEach((item, index) => {
        if (index === 0 && this.hasChild(item)) {
          customStyle += `
          .btn-item-${index}.checked .btn-class-showable .btn-child-parent {
            transform: translateX(${(item.childs.length * 45) / 2 - 35}px);
            transition: transform 500ms ease 300ms;
          }
          `;
        }

        if (index === this.options.length - 1 && this.hasChild(item)) {
          customStyle += `
          .btn-item-${index}.checked .btn-class-showable .btn-child-parent {
            transform: translateX(-${(item.childs.length * 45) / 2 - 35}px);
            transition: transform 500ms ease 300ms;
          }
          `;
        }

        customStyle += `
        .btn-item-${index} {
          padding: 10px;
          transition: transform 100ms ease;
          width : ${containerWidth / this.options.length}px !important;
          display: flex;
          justify-content :center;
          align-items : center;
          position: relative;
          z-index: 10;
        }

        `;

        if (this.hasChild(item)) {
          item.childs.forEach((child, idx) => {
            customStyle += `
            .btn-item-${index}.checked .btn-class-showable .btn-child:nth-child(${
              idx + 1
            }) {
              transform: translateX(${
                (0.5 + idx) * 45 - (item.childs.length * 45) / 2
              }px);
              transition: transform 500ms ease 300ms;
            }
          `;
          });
        }
      });

      document.getElementById('sweep').style.left = `
      ${containerWidth / this.options.length / 4 - 135 / 2}px`;

      const head = document.getElementsByTagName('head')[0];
      const style = document.createElement('style');
      style.id = 'bottom-navigation-style';

      if (style.styleSheet) {
        style.styleSheet.cssText = customStyle;
      } else {
        style.appendChild(document.createTextNode(customStyle));
      }

      head.appendChild(style);
    },
    handleLabelClick(button) {
      if (!this.showable || button.isActive) {
        this.toggleClass();
      }

      this.updateValue(button, this.hasChild(button));
    },
    handleChildClick(button) {
      this.updateValue(button);
      this.toggleClass();
    },
    updateValue(button, prevent = false) {
      this.localOptions.forEach(
        (option) => (option.isActive = this.isActive(option, button.id))
      );

      if (!prevent) {
        this.$emit('update', button.id);
        this.enableWatch = false;
        setTimeout(() => {
          this.enableWatch = true;
        }, 0);

        if (button.path && Object.keys(button.path).length) {
          if (this.replaceRoute) {
            this.$router.replace(button.path).catch(() => {});
          } else {
            this.$router.push(button.path);
          }
        }
      }
    },
    toggleClass() {
      this.showable = !this.showable;
    },
    isActive(button, value = this.value) {
      return (
        button.id == value ||
        (button.childs || []).find((child) => child.id == value)
      );
    },
    onResize() {
      this.$nextTick(() => {
        const styleElement = document.getElementById('bottom-navigation-style');
        styleElement && styleElement.remove();
      });

      this.cssLoader();
    },
    hasChild(button) {
      return (button.childs || []).length;
    }
  }
};
</script>

<style scoped>
.btn-super-parent {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  bottom: 55px;
  width: var(--width-parent);
  height: 60px;
  z-index: -1;
}

input {
  display: none;
}

.btn-item-2.checked ~ #sweep {
  transform: translateX(162px);
  transition: transform 500ms ease;
}

.btn-container_foreground {
  position: fixed;
  direction: ltr;
  display: flex;
  align-items: flex-end;
  bottom: 0;
  width: 100%;
  z-index: 2147483647;
  height:65px;
  border-color: rgba(209,213,219,1);
  background: var(--color-foreground);
}

.btn-item-2{
  height: 348px;
  display: flex;
  flex: 1;
  background: transparent;
  border-radius: 0 0 45% 45%;
}

.btn-container {
  direction: ltr;
  display: flex;
  justify-content: space-around;
  background-color: var(--color-background);
  width: 100%;
  height:60px;
}

.active-label {
  width: 35px;
  height: 35px;
  border-radius: 40%;
  display: flex;
  justify-content: center;
  align-items: center;
  transition: all 300ms ease;
  position: absolute;
  top: 10px;
  background: #1e74d6;
  color: var(--color-icon);
}

.btn-title {
  position: absolute;
  color: var(--color-icon);
  font-size: 12px;
  font-weight: 700;
  line-height: 1.15 !important;
}

.btn-badge {
  width: 18px;
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: 0px;
  left: 25px;
  border-radius: 50%;
  font-size: 12px;
  color: #fff;
  background: var(--color-badge);
}

.checked .active-label {
  /* Up icon */
  transform: translateY(-10px);
}

.btn-item-2 .active-label{
  transform: translateY(-18px);
}

.checked .btn-title {
  animation: fadein 200ms;
  position: absolute;
  top: 38px;
}

.unchecked .active-label {
  background: transparent;
}

.unchecked .btn-title {
  visibility: hidden;
}

#sweep {
  height: 100%;
  width: 135px;
  display: flex;
  position: absolute;
  left: 0;
  top: 0px;
}

#sweep-center {
  height: 38px;
  display: flex;
  flex: 1;
  background-color: rgb(243 244 246 / 1);
  border-radius: 0 0 45% 45%;
}

#sweep-left {
  height: 33px;
  width: 45px;
  overflow: hidden;
  position: relative;
  right: 2px;
}

#sweep-left:before {
  content: '';
  display: block;
  width: 220%;
  height: 200%;
  position: absolute;
  border-radius: 50%;
  top: 0;
  left: 0;
  box-shadow: -40px -40px 0 0 var(--color-foreground);
}

#sweep-right {
  height: 33px;
  width: 45px;
  overflow: hidden;
  position: relative;
  left: 2px;
}

#sweep-right:before {
  content: '';
  display: block;
  width: 220%;
  height: 200%;
  position: absolute;
  border-radius: 50%;
  top: 0;
  right: 0;
  box-shadow: 40px -40px 0 0 var(--color-foreground);
}

@media screen and (min-width: 576px) {
  .labels {
    cursor: pointer;
  }
}

@keyframes fadein {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0px);
  }
}

/* child */

.btn-child-badge {
  width: 18px;
  height: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: absolute;
  top: -4px;
  left: 20px;
  border-radius: 50%;
  font-size: 12px;
  color: #fff;
  background: var(--color-badge);
  opacity: 0;
}

.btn-child-parent {
  position: absolute;
  bottom: -60px;
  width: 35px;
  height: 35px;
  border-radius: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
  background: var(--color-foreground);
}

.btn-child {
  position: absolute;
  height: 30px;
  width: 30px;
  border-radius: 50%;
  background: var(--color-background);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  color: var(--color-icon);
}
.btn-child-title {
  font-size: 10px;
  opacity: 0;
  position: absolute;
  top: 37px;
  color: rgba(17,24,39,1);
  line-height: 1.15 !important;
}

.unchecked .btn-child-parent {
  background: transparent;
}

.checked .btn-class-showable .btn-child-parent {
  animation: child-background 500ms ease-in-out forwards;
}

.checked .btn-class-showable .btn-child-title {
  animation: child-title 500ms ease-in-out forwards;
}

.checked .btn-class-showable .btn-child-badge {
  animation: child-title 500ms ease-in-out forwards;
}

@keyframes child-title {
  50% {
    opacity: 0;
  }
  100% {
    opacity: 1;
  }
}

@keyframes child-background {
  0% {
    bottom: -30px;
    background: transparent;
  }

  25% {
    bottom: 20px;
    width: 35px;
    height: 35px;
  }

  40% {
    bottom: 20px;
    width: 35px;
    height: 40px;
  }

  100% {
    bottom: 20px;
    width: 100%;
    height: 40px;
  }
}
</style>
