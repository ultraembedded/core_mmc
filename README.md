### MMC (and derivative standards) Host Controller

Github:   [https://github.com/ultraembedded/core_mmc](https://github.com/ultraembedded/core_mmc)

Work-in-progress - basically functional but not yet complete / robust.

##### Features
* 1-bit / 4-bit data modes.
* Large sector buffer (for multiple sector reads or writes).
* AXI-4 DMA.

##### Current Bugs
* DMA: Does not support card write mode (functions as read from card only).
* Robustness: Not currently checking CRC7 / CRC16 on incoming responses.
* Writes: Multi-sector write support is not correct.
* AXI: Dubious combinatorial paths on AWVALID and WVALID.

##### Testing
Exercised on the following FPGA boards;
* Digilent Arty A7 (Xilinx Artix 7)
* LambaConcept ECPIX-5 (Lattice ECP5)

##### Register Map

| Offset | Name | Description   |
| ------ | ---- | ------------- |
| 0x00 | MMC_CONTROL | [RW] Transfer Control Register |
| 0x04 | MMC_CLOCK | [RW] Clock Configuration Register |
| 0x08 | MMC_STATUS | [R] Transfer Status Register |
| 0x0c | MMC_CMD0 | [RW] Command (first 32-bits) |
| 0x10 | MMC_CMD1 | [RW] Command (subsequent 16-bits) |
| 0x14 | MMC_RESP0 | [R] Response Register |
| 0x18 | MMC_RESP1 | [R] Response Register |
| 0x1c | MMC_RESP2 | [R] Response Register |
| 0x20 | MMC_RESP3 | [R] Response Register |
| 0x24 | MMC_RESP4 | [R] Response Register |
| 0x28 | MMC_TX | [W] Data Transmit Register |
| 0x2c | MMC_RX | [R] Data Receive Register |
| 0x30 | MMC_DMA | [RW] DMA Target |

##### Register: MMC_CONTROL

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31 | START | Start transfer. |
| 30 | ABORT | Abort transfer. |
| 29 | FIFO_RST | FIFO reset. |
| 15:8 | BLOCK_CNT | Number of blocks (0=1, 1=2, ...) |
| 5 | WRITE | Data write operation |
| 4 | DMA_EN | DMA port enable |
| 3 | WIDE_MODE | 4-bit data mode. |
| 2 | DATA_EXP | Wait for data |
| 1 | RESP136_EXP | Wait for response (R2). |
| 0 | RESP48_EXP | Wait for response (~R2). |

##### Register: MMC_CLOCK

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 7:0 | DIV | Clock divider |

##### Register: MMC_STATUS

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 8 | CMD_IN | Command input line state |
| 7:4 | DAT_IN | Data input line state |
| 3 | FIFO_EMPTY | FIFO empty. |
| 2 | FIFO_FULL | FIFO full. |
| 1 | CRC_ERR | CRC error |
| 0 | BUSY | Transfer active |

##### Register: MMC_CMD0

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | VALUE | Command data. |

##### Register: MMC_CMD1

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 15:0 | VALUE | Command data. |

##### Register: MMC_RESP0

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | VALUE | Response data. |

##### Register: MMC_RESP1

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | VALUE | Response data. |

##### Register: MMC_RESP2

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | VALUE | Response data. |

##### Register: MMC_RESP3

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | VALUE | Response data. |

##### Register: MMC_RESP4

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | VALUE | Response data. |

##### Register: MMC_TX

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | DATA | Data |

##### Register: MMC_RX

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | DATA | Data |

##### Register: MMC_DMA

| Bits | Name | Description    |
| ---- | ---- | -------------- |
| 31:0 | ADDR | Start address |

