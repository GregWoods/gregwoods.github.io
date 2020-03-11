---
layout: single
classes: wide
title:  "Rust syntax highlighting"
date:   2020-03-10 17:58:31 +0000
categories: rust test
---

# Rust Sample

{% highlight ruby linenos %}
#[entry]
fn main() -> ! {
    if let (Some(p), Some(cp)) = (stm32::Peripherals::take(), Peripherals::take()) {
        // Constrain clocking registers
        let mut flash = p.FLASH;
        let mut rcc = p.RCC.configure().sysclk(48.mhz()).freeze(&mut flash);
        let gpioa = p.GPIOA.split(&mut rcc);

        /* (Re-)configure PA7 as output */
        let ws_data_pin =
            cortex_m::interrupt::free(move |cs| gpioa.pa7.into_push_pull_output_hs(cs));

        let timer = Timer::tim1(p.TIM1, MegaHertz(3), &mut rcc);

        // Get delay provider
        let mut delay = Delay::new(cp.SYST, &mut rcc);

        let mut ws = Ws2812::new(timer, ws_data_pin);
        let mut data: [RGB8; 3] = [RGB8::default(); 3];
        let empty: [RGB8; 3] = [RGB8::default(); 3];

        data[0] = RGB8 {
            r: 0,
            g: 0,
            b: 0x10,
        };
        data[1] = RGB8 {
            r: 0,
            g: 0x10,
            b: 0,
        };
        data[2] = RGB8 {
            r: 0x10,
            g: 0,
            b: 0,
        };

        loop {
            ws.write(data.iter().cloned()).unwrap();
            delay.delay_ms(10 as u16);
            ws.write(empty.iter().cloned()).unwrap();
            delay.delay_ms(10 as u16);
        }
    }
    loop {
        continue;
    }
}
{% endhighlight %}
